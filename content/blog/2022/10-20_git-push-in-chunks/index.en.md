+++
date = "2022-10-20"
title = "Chunked git-push into Azure DevOps"
tags = ["Git", "Azure DevOps", "Azure"]
image = "blog-2022-11.png"
+++

The other day I encountered a fun little problem while trying to import a large git repository into [Azure DevOps]:

> Very large pushes use up a lot of resources, blocking or slowing
> other parts of the service. Such pushes often don't map to normal
> software development activities. Someone may have inadvertently
> checked in build outputs or a VM image, for example. For these
> reasons and more, `pushes are limited to 5GB at a time`.
>
> -- <cite>[Azure DevOps Documentation][1] (emphasis mine)</cite>

So, well .. this sucks as my repository at hand is way bigger than 5GB :cry:

### :x: Solution: Web Import

What does Microsoft suggest as a solution? Just import the git repository via the [web import feature][2]!

Sadly this **was not an option** as the source git repository is not directly accessible by [Azure DevOps] :cry: :cry:

### :white_check_mark: Solution: Chunked `git push`

Well, as you might have noticed only **a single push** can not exceed the 5GB limit as the repository itself can easily grow up to 250GB.

Ha! Now we have an angle of attack! We simply push our repository in small chunks, ensure that we never exceed the limit for a single `git push` and some time later we should arrive at the current `HEAD` :sunglasses:

And with the power of bash the whole taks was as simple as:

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

In my case it was enought to run this once on the `master` branch, as the final `git push --mirror` will push everything else (tags and all other branches).

> **:bell: Warning :bell:**
>
> The last `git push --mirror` might also run into the same 5GB limit if you have a lot and/or big commits outside the `master` branch!
> If so, just repeat the steps from above until `git push --mirror` also stays within the limit.


  [Azure DevOps]: https://azure.microsoft.com/en-us/products/devops/
  [1]: https://learn.microsoft.com/en-us/azure/devops/repos/git/limits?view=azure-devops#push-size
  [2]: https://learn.microsoft.com/en-us/azure/devops/repos/git/import-git-repository?view=azure-devops#import-into-a-new-repo