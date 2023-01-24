+++
date = "2022-10-20"
title = "Gestückeltes git-push nach Azure DevOps"
tags = ["Git", "Azure DevOps", "Azure"]
+++

Die Tage hatte ich ein lustiges kleines Problem bei dem Versuch ein großes Git Repository nach [Azure DevOps] zu importieren:

> Sehr große Pushs verwenden viele Ressourcen, blockieren oder
> verlangsamen andere Teile des Diensts. Solche Pushs werden
> häufig nicht zu normalen Softwareentwicklungsaktivitäten
> zugeordnet. Jemand hat möglicherweise versehentlich in Buildausgaben
> oder ein VM-Image eingecheckt, z. B. Aus diesen Gründen und mehr
> sind <ins>Pushs auf 5 GB zu einem Zeitpunkt beschränkt</ins>.
>
> -- <cite>[Azure DevOps Dokumentation][1] (hervorhebung von mir)</cite>

Also .. uhm .. naja, das ist nun doof, da mein Repository halt größer ist als 5GB :cry:

## :x: Lösung: Web Import

Welche Lösung schlägt Microsoft hier vor? Man soll das Git Repository einfach über ein [web import][2] laufen lassen!

Leider war **das keine Option**, da das Quellsystem (auf dem das Git Repository primär gehosted ist) für [Azure DevOps] nicht direkt erreichbar war (Firewall und so) :cry: :cry:

## :white_check_mark: Lösung: Gestückeltes `git push`

Nun, wenn man die Dokumentation aufmerksam liest, dann merkt man das **ein einzelnes `git push`** nicht größer sein darf als 5GB. Das komplette Repository kann aber bis auf 250GB anwachsen.

Ha! Hier können wir also ansetzen! Wir schieben unser Repository einfach in kleinen Stücken nach [Azure DevOps], bleiben immer unter den 5GB und nach einigen Runden `git push` haben wir alles drüben.

Mit einem bisschen `bash` klappt das wie folgt:

```bash
$ # Ensure we're starting from the master branch
$ git checkout master

$ # First we need to count the total amount of commits
$ TOTAL_COMMITS=$(git log --pretty=oneline | wc -l)

$ # How many commits should be in a single chunk?
$ COMMITS_PER_CHUNK=50

$ # Push our commits in small chunks
$ for CURSOR in $(seq $TOTAL_COMMITS -$COMMITS_PER_CHUNK 0); do \
    git push origin master~$CURSOR:master;  \
  done

$ # And finally push the missing rest (tags, etc.)
$ git push --mirror origin
```

In meinem Fall war es ausreichend das ganze einmal auf dem `master` Branch laufen zu lassen, da sich das finale `git push --mirror` um den ganzen fehlenden Rest (tags und andere Branches) gekümmert hat.

{{< alert >}}
Das letzte `git push --mirror` kann auch in die 5GB Grenze laufen, wenn es viele / große Commits außerhalb von dem `master` branch gibt!
In dem Fall wiederholt man die Schritte in einem anderen Branch bis `git push --mirror` dann ebenfalls durchläuft.
{{</ alert >}}

  [Azure DevOps]: https://azure.microsoft.com/de-de/products/devops/
  [1]: https://learn.microsoft.com/de-de/azure/devops/repos/git/limits?view=azure-devops#push-size
  [2]: https://learn.microsoft.com/de-de/azure/devops/repos/git/import-git-repository?view=azure-devops#import-into-a-new-repo
