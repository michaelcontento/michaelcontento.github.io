+++
date = "2022-11-30"
title = "Ein Spiel an einem Tag"
tags = ["PlayDate", "Lua", "Gaming", "InnovationDay"]
categories = ["Development", "Gaming"]
+++

Am 25.11.2022 fand der zweite Innovation Day @ [Xpirit] statt und es war der erste, an dem ich einen eigenen Slot gestarte habe.

Aber was ist der Innovation Day überhaupt? <!--more--> Es ist ein vierteljährliches Treffen, bei dem sich alle Mitglieder von Xpirit **physisch** treffen und entwickeln, erforschen, spielen und Wissen teilen. Betrachten es als einen Hackathon im Kreise der Familie 😄

Um den Tag ein bisschen zu organisieren, haben wir unser eigenes internes Tool [XKE] (**X**ebia **K**nowledge **E**xchange), wo jeder mit seiner Idee einen neuen Slot starten kann und andere können beitreten. Es ist wirklich so einfach. Such dir ein Thema oder starte ein neues.

## PlayDate - ein kleines Handheld-Spielsystem

Zwei Tage vor dem Innovation Day stellte mir mein Kollege [Thomas] das [PlayDate] vor und ich war sofort begeistert.

Wie großartig ist dieses winzige Gerät? Ernsthaft.

Kleiner Bildschirm mit `400 x 240` Pixeln, zwei Farben und eine echten physische Kurbel!

Sicher, das sind ziemlich strenge Beschränkungen im Vergleich zu allen anderen Spielsystemen – aber Beschränkungen regen die Kreativität an! Zumindest lese ich das immer im Internet ... 😉

## Mein erster Innovation Day Slot

Also war das Feuer entfacht und ich wollte unbedingt etwas für dieses Gerät bauen. Aber mit 2 Tagen war es unmöglich, rechtzeitig ein physisches Gerät zu bestellen.

Aber die Community hinter PlayDate ist ziemlich großartig und der kostenlos nutzbare Simulator ist ... naja ... awesome! Es ist wirklich Plug-and-Play (oder herunterladen und ausführen, um genauer zu sein).

Für den [Nova]-Editor gibt es eine [Erweiterung][1], die ebenfalls wunderbar funktioniert. Obwohl ich Nova oder PlayDate noch nie zuvor verwendet habe, waren es nur ein paar Downloads, Mausklicks und alles kompilierte und lief reibungslos.

Also haben wir einen Plan: [Wir bauen ein einigermaßen unterhaltsames Spiel für die PlayDate-Konsole!][2]

## Was wollen wir eigentlich bauen?

Am Innovation Day fanden sich 3 Kollegen, die meine Idee mochten und sich meinem Slot anschließen. Nun mussten wir ein paar Dinge klären:

1) Der Simulator muss auf jedem Entwicklercomputer laufen
2) Wir brauchen ein Git-Repository, in dem wir alle arbeiten können
3) Definieren, welches Spiel wir eigentlich bauen wollen
4) Code Code Code
5) Unsere Erfahrung mit den anderen Teilen
6) 🍻

Die ersten zwei Punkte der Liste wurden in ~20 Minuten erledigt. Wie ich schon sagte, die Tools sind Plug-and-Play und mit [Playlate] haben wir eine tolle Projektvorlage gefunden.

Zu definieren, **was** wir eigentlich bauen wollen, hat etwas länger gedauert. Ich meine, man könnte im Grunde alles auf diesem Gerät bauen! Alleine mit der Kurbel eröffnen sich hundert verschiedene kreative Möglichkeiten! Tausende Ideen!

Aber unsere Zeit war begrenzt. Und wir wollten etwas erschaffen, das so grob 10 Sekunden Freude bereiten kann.

Warum nicht ein einfaches & bekanntes Spiel klonen und nur eine kleine Twist hinzufügen? Ha! Das ist es!

Als Spiel haben wir uns für [FlappyBird] entschieden und wollten die Kurbel einbauen, um „echtes Flattern“ zu simulieren. Man muss also, für einen einzelnen Flügelschlag, einmal hin und her schwingen.

## Das Ergebnis

{{< youtube Scehich_JLM >}}

- Es ist ein voll funktionsfähiger Klon von FlappyBird
- Läuft flüssig bei maximaler FPS ohne jegliche Probleme
- Wir haben Hintergrundmusik sowie Soundeffekte
- Sprite-Animationen
- Endlose Level-Generierung
- Highscore
- Kollisionserkennung

Alles an einem Tag gebaut - ich bin so stolz auf unsere Gruppe und unser kleines Maskottchen 🧡

## Was haben wir gelernt?

- Das Bauen von Spielen macht Spaß
- PlayDate ist ein sehr schönes / ausgefeiltes Spielsystem
- Wir haben [Lua] als Entwicklungssprache verwendet
- Wir haben [FFmpeg] verwendet, um Audiodateien in das richtige Format zu konvertieren
- Und wir hatten eine Menge Spaß beim Bauprozess selbst


   [Lua]: https://www.lua.org/
   [FFmpeg]: https://ffmpeg.org/
   [FlappyBird]: https://flappybird.io/
   [Playlate]: https://github.com/downie/playlate
   [Nova]: https://nova.app
   [1]: https://extensions.panic.com/extensions/com.panic/com.panic.Playdate/
   [2]: https://xke.xebia.com/event/UiHeo6yw3MS6LsnUAEj1/Bd81zbPqzHnTwiP5hFrk/xpirit-game-on-playdate
   [Thomas]: https://tomow.de/
   [PlayDate]: https://play.date/
   [Xpirit]: https://xpirit.com
   [XKE]: https://xke.xebia.com/event/UiHeo6yw3MS6LsnUAEj1
