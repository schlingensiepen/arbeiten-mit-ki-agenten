# Git als Gedächtnis

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `MasterPrompt.md`.

Das Kapitel [Kontext](A020-kontext.md) hat eine Regel aufgestellt: Was Sie ausarbeiten, gehört in Dateien. Dateien haben aber eine Schwäche. Sie zeigen nur ihren letzten Stand. Ein Agent ändert in einer Sitzung Dutzende Dateien, schnell und ohne dass Sie jede Änderung sehen. Morgen wissen Sie nicht mehr, was gestern anders war, und wenn eine Änderung falsch war, ist die alte Fassung weg. Dafür gibt es seit langem ein Werkzeug, und es ist nichts Weltbewegendes: [Git](../Z-anhang/Z010-glossar.md#git) zeichnet die Geschichte eines Projekts auf. Jede Änderung bleibt nachvollziehbar und lässt sich zurücknehmen. Dieses Kapitel gibt Ihnen die Handvoll Befehle, die Sie dafür brauchen, und erklärt, wie ein Agent mit Git umgeht. Alles, was in diesem Skript später auf gesicherter Arbeit aufbaut, setzt dieses Kapitel voraus.

## Repo und Commit

Ein Projektordner, den Git beaufsichtigt, heißt [Repo](../Z-anhang/Z010-glossar.md#repo), kurz für Repository. Äußerlich ist es ein gewöhnlicher Ordner; Git legt darin einen versteckten Unterordner `.git` an, in dem die ganze Geschichte liegt. Diese Geschichte besteht aus [Commits](../Z-anhang/Z010-glossar.md#commit). Ein Commit ist ein gesicherter Zwischenstand aller Dateien mit einer Beschreibung, was sich geändert hat, mit Ihrem Namen und dem Zeitpunkt. Zu jedem Commit lässt sich zurückkehren.

Git sichert nicht von selbst. Es merkt sich nur, was Sie ihm ausdrücklich übergeben. Das ist gewollt: Ein Commit soll ein Zwischenstand sein, den jemand für sinnvoll hielt, nicht ein Schnappschuss alle fünf Minuten.

## Die ersten Befehle

Bevor der erste Commit entsteht, trägt Git Ihren Namen ein, einmal für alle Projekte:

```bash
git config --global user.name "Vorname Nachname"
git config --global user.email "name@example.org"
```

Die E-Mail-Adresse steht danach in jedem Commit. In einem öffentlichen Projekt kann sie jeder lesen. GitHub bietet dafür eine Ersatzadresse an, die auf `users.noreply.github.com` endet; tragen Sie diese ein, wenn Sie Ihre Adresse nicht veröffentlichen wollen.

Dann im Projektordner, am Beispiel der Lagerverwaltung:

```bash
cd ~/source/sandbox/lager
git init                                   # macht den Ordner zum Repo, einmalig
git status                                 # was hat sich seit dem letzten Commit geändert
git add .                                  # alle Änderungen für den nächsten Commit vormerken
git commit -m "Anforderungen: erste Fassung"   # das Vorgemerkte sichern, mit Beschreibung
git log --oneline                          # die Geschichte, ein Commit je Zeile
```

`git status` werden Sie am häufigsten tippen. Es sagt, welche Dateien neu sind, welche geändert und welche noch nicht vorgemerkt. `git add .` merkt alles vor, `git commit` sichert das Vorgemerkte. Die Beschreibung nach `-m` ist für den Menschen, der die Geschichte später liest, oft Sie selbst. Schreiben Sie hinein, was sich geändert hat, nicht „Update“.

Im Container von clawbook ist jedes Projekt unter `~/source` schon als Repo angelegt, wenn es mit `wsm` entstanden ist; dann entfällt `git init`.

## Zurückgehen

Der Grund für den ganzen Aufwand. Drei Fälle, vom harmlosen zum ernsten:

**Sie wollen sehen, was sich geändert hat.** `git diff` zeigt alle Änderungen seit dem letzten Commit, Zeile für Zeile. `git diff anforderungen.md` nur für eine Datei. Wenn der Agent gerade zwanzig Minuten gearbeitet hat, ist das der Blick darauf, was er getan hat.

**Eine Änderung war falsch, der letzte Commit war gut.** `git restore anforderungen.md` setzt die Datei auf den Stand des letzten Commits zurück. Alles, was seitdem an ihr geändert wurde, ist weg, also vorher mit `git diff` hinsehen.

**Die gute Fassung liegt weiter zurück.** Suchen Sie in `git log --oneline` den Commit, in dem die Datei noch stimmte; vorn steht eine kurze Kennung aus Ziffern und Buchstaben. Dann:

```bash
git show a1b2c3d:anforderungen.md          # die alte Fassung ansehen, ohne etwas zu ändern
git checkout a1b2c3d -- anforderungen.md   # die alte Fassung in den Ordner holen
git commit -m "Anforderungen: Fassung vom Vortag wiederhergestellt"
```

Die Kennung `a1b2c3d` ersetzen Sie durch die aus Ihrem Log. Die Wiederherstellung ist selbst wieder ein Commit, die Geschichte bleibt vollständig. Nichts, was einmal in einem Commit war, geht verloren. Was nie in einem Commit war, kennt Git nicht. Das ist der Satz, den Sie aus diesem Kapitel mitnehmen sollten.

## GitHub

Bis hierher liegt die Geschichte nur auf Ihrem Rechner. [GitHub](../Z-anhang/Z010-glossar.md#github) ist ein Dienst im Netz, auf dem Repos liegen, gesichert und für andere erreichbar. Mit `git push` schicken Sie Ihre Commits dorthin, mit `git clone` holen Sie ein Repo auf einen anderen Rechner. Für Git selbst ist GitHub nicht nötig, für Sie aus zwei Gründen nützlich: Geht der Rechner verloren, ist das Projekt noch da, und andere können es lesen. GitHub zeigt Markdown-Dateien direkt lesbar an; deshalb ist auch die Beschreibung eines Projekts, die `README.md`, eine Markdown-Datei.

Im Container von clawbook haben Sie sich beim ersten Verbinden bei GitHub angemeldet. `wsm` legt neue Projekte gleich dort an, und `git push` funktioniert ohne weitere Anmeldung.

## Wie der Agent mit Git umgeht

Alles bisher können Sie dem Agenten überlassen. „Sichere die Arbeit mit Git“ genügt, er kennt die Befehle. Nützlicher ist, wenn er es von selbst tut, und zwar nach festen Regeln. Solche Regeln stehen in einem [Regelwerk](../Z-anhang/Z010-glossar.md#regelwerk), den Dateien, die festlegen, wie ein Agent in einem Projekt arbeitet. Wie ein Regelwerk in ein Projekt kommt, zeigt der Teil [Wissen im Wiki](../D-wissen-im-wiki/D020-regelwerk-und-sessionstart.md). Was es für Git festlegt, lässt sich schon jetzt verstehen:

- **Ein Commit je Zug.** Ein Zug ist eine thematisch abgeschlossene Einheit aus mehreren Arbeitsschritten, etwa „Anforderungen überarbeitet“. Der Agent sichert nach jedem Zug, nicht erst am Ende, und bündelt keine drei Züge in einem Commit. So bleibt die Geschichte lesbar und jeder Zwischenstand erreichbar.
- **Eine Nachricht mit Präfix.** Jede Commit-Nachricht beginnt mit einem Wort, das sagt, welcher Art die Änderung ist, dann ein Doppelpunkt und die Kurzbeschreibung. In der Geschichte sieht man so auf einen Blick, wo Dokumentation geändert wurde und wo Code.
- **Ein abschließender Commit am Ende der Sitzung.** Was die Züge nicht erfasst haben, sichert der Agent zum Schluss, damit die Sitzung mit einem sauberen Ordner endet.
- **Keine Geheimnisse.** Zugangsdaten, Passwörter und Schlüssel gehören in keine Datei, die in einen Commit kommt. Was einmal in der Geschichte liegt, bleibt dort, auch wenn man es später aus der Datei löscht.
- **Kein Push ohne Anweisung.** Der Agent schickt nichts von sich aus nach GitHub. Was den Rechner verlässt, entscheiden Sie.

## Warum das jetzt zählt

Zurück zur offenen Frage aus dem Kapitel [Die erste Sitzung](A040-die-erste-sitzung.md). Dort hieß es, ein Agent dürfe nur dann ohne Rückfragen arbeiten, wenn der Rechner wegwerfbar und die Arbeit per Git gesichert ist. Jetzt können Sie die zweite Bedingung prüfen. Gesichert heißt: Die Arbeit ist in einem Commit, und der Commit ist auf GitHub. Dann kann ein Agent, der eine Datei zerstört, höchstens die Arbeit seit dem letzten Commit kosten. Was er dagegen außerhalb des Repos anrichtet, an Anmeldungen, an anderen Ordnern, an Ihrem Rechner, kann Git nicht zurückholen. Das ist die erste Bedingung, und sie ist die schwerere.

## Was jetzt klar sein sollte

- Git zeichnet die Geschichte eines Projekts auf, in Commits. Ein Repo ist ein Ordner mit dieser Geschichte.
- Fünf Befehle reichen für den Anfang: `status`, `add`, `commit`, `log`, `diff`. Zum Zurückgehen `restore` und `checkout` mit der Kennung eines Commits.
- Nichts, was in einem Commit war, geht verloren. Was nie in einem Commit war, kennt Git nicht.
- GitHub bewahrt die Geschichte außerhalb Ihres Rechners auf und macht sie lesbar.
- Ein Agent sichert nach Regeln: je Zug ein Commit, Nachricht mit Präfix, keine Geheimnisse, kein Push ohne Anweisung.

Damit ist Teil A zu Ende. Sie haben einen laufenden Agenten, wissen, was er ist, warum sein Kontext begrenzt ist, und Ihre Arbeit ist gesichert. Weiter mit [Anforderungen im Gespräch](../B-der-naive-ansatz/B010-anforderungen-im-gespraech.md): Sie bauen mit dem Agenten das erste Programm, auf dem direkten Weg.
