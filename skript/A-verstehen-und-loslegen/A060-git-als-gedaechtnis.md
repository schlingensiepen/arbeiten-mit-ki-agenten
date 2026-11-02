# Git als Gedächtnis

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `MasterPrompt.md`; [clawbook-lehre](https://github.com/schlingensiepen/clawbook-lehre) `main`, `docs/setup/github.md`.

Das Kapitel [Kontext](A020-kontext.md) hat eine Regel aufgestellt: Was Sie ausarbeiten, gehört in Dateien. Dateien haben aber eine Schwäche. Sie zeigen nur ihre letzte Fassung. Ein Agent ändert in einer Sitzung Dutzende Dateien, schnell und ohne dass Sie jede Änderung sehen. Morgen wissen Sie nicht mehr, was gestern anders war, und wenn eine Änderung falsch war, ist die alte Fassung weg. Dafür gibt es seit langem ein Werkzeug, und es ist nichts Weltbewegendes: [Git](../Z-anhang/Z010-glossar.md#git) zeichnet die Geschichte eines Projekts auf. Jede gesicherte Änderung bleibt nachvollziehbar und lässt sich zurücknehmen. Dieses Kapitel gibt Ihnen die Handvoll Befehle, die Sie dafür brauchen, und erklärt, wie ein Agent mit Git umgeht. Alles, was in diesem Skript später auf gesicherter Arbeit aufbaut, setzt dieses Kapitel voraus.

## Repo und Commit

Ein Projektordner, den Git beaufsichtigt, heißt [Repo](../Z-anhang/Z010-glossar.md#repo), kurz für Repository. Äußerlich ist es ein gewöhnlicher Ordner; Git legt darin einen versteckten Unterordner `.git` an, in dem die ganze Geschichte liegt. Diese Geschichte besteht aus [Commits](../Z-anhang/Z010-glossar.md#commit). Ein Commit ist eine gesicherte Fassung aller Dateien mit einer Beschreibung, was sich geändert hat, mit Ihrem Namen und dem Zeitpunkt. Zu einem Commit lässt sich später zurückkehren.

Git sichert nicht von selbst. Es merkt sich nur, was Sie ihm ausdrücklich übergeben. Das ist gewollt: Ein Commit soll ein Zwischenergebnis sein, das jemand für sinnvoll hielt, nicht ein Schnappschuss alle fünf Minuten.

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
git status                                 # welche Dateien sind neu, geändert, vorgemerkt
git add .                                  # alle Änderungen für den nächsten Commit vormerken
git commit -m "Anforderungen: erste Fassung"   # das Vorgemerkte sichern, mit Beschreibung
git log --oneline                          # die Geschichte, ein Commit je Zeile
```

`git status` werden Sie am häufigsten tippen. Es nennt nur die Dateien: welche neu sind, welche geändert und welche schon vorgemerkt. Was sich darin geändert hat, zeigt es nicht. `git add .` merkt alles vor, `git commit` sichert das Vorgemerkte. Die Beschreibung nach `-m` ist für den Menschen, der die Geschichte später liest, oft Sie selbst. Schreiben Sie hinein, was sich geändert hat, nicht „Update“.

Im Container von clawbook ist jedes Projekt unter `~/source` schon als Repo angelegt, wenn es mit `wsm` entstanden ist; dann entfällt `git init`. Den Ordner `lager` haben Sie von Hand angelegt, für ihn brauchen Sie den Befehl.

## Zurückgehen

Der Grund für den ganzen Aufwand. Drei Fälle, vom harmlosen zum ernsten:

**Sie wollen sehen, was sich geändert hat.** Dafür gibt es zwei Befehle, je nachdem, ob die Änderung schon in einem Commit liegt:

```bash
git diff                      # Änderungen, die noch nicht vorgemerkt sind, Zeile für Zeile
git diff anforderungen.md     # dasselbe für eine Datei
git log -p                    # die Commits, jeder mit seinen Änderungen, die neuesten zuerst
git log -p anforderungen.md   # dasselbe für eine Datei
```

`git diff` zeigt nur, was noch nicht vorgemerkt ist. Nach `git add` bleibt die Ausgabe leer, und eine neue Datei, die Git noch nicht kennt, taucht darin nicht auf; die nennt `git status`. Wenn der Agent gerade zwanzig Minuten gearbeitet hat, sehen Sie mit `git diff`, was er noch nicht gesichert hat, und mit `git log -p`, was er schon gesichert hat. Lange Ausgaben zeigt Git seitenweise. Mit den Pfeiltasten blättern Sie, mit `q` beenden Sie die Anzeige.

**Eine Änderung war falsch, der letzte Commit war gut.** `git restore anforderungen.md` verwirft die noch nicht vorgemerkten Änderungen an der Datei. Ohne Vormerkung kommt so die Fassung des letzten Commits zurück. Haben Sie die Datei mit `git add` schon vorgemerkt, führt der Befehl nur zur vorgemerkten Fassung. Dann nehmen Sie zuerst die Vormerkung zurück:

```bash
git restore --staged anforderungen.md   # die Vormerkung zurücknehmen
git restore anforderungen.md            # die Datei auf die Fassung des letzten Commits setzen
```

Eine Datei, die nie in einem Commit war, kann `git restore` nicht wiederherstellen. Und was der Befehl verwirft, ist weg, auch Git holt es nicht zurück. Sehen Sie also vorher mit `git diff` hin.

**Die gute Fassung liegt weiter zurück.** Suchen Sie in `git log --oneline` den Commit, in dem die Datei noch stimmte; vorn steht eine kurze Kennung aus Ziffern und Buchstaben. Dann:

```bash
git show a1b2c3d:anforderungen.md          # die alte Fassung ansehen, ohne etwas zu ändern
git checkout a1b2c3d -- anforderungen.md   # die alte Fassung in den Ordner holen
git commit -m "Anforderungen: Fassung vom Vortag wiederhergestellt"
```

Die Kennung `a1b2c3d` ersetzen Sie durch die aus Ihrem Log. Die Wiederherstellung ist selbst wieder ein Commit, die älteren Commits bleiben erhalten. Was nie in einem Commit war, kennt Git nicht. Das ist der Satz, den Sie aus diesem Kapitel mitnehmen sollten.

Umgekehrt ist ein Commit kein Tresor. Die Geschichte liegt als Dateien im Ordner `.git`, und Git hat Befehle, die Commits aus der Geschichte entfernen, etwa `git reset --hard`. Ein Agent kann solche Befehle ausführen oder den Ordner löschen, aus Versehen oder weil ein Text im Kontext ihn dazu bringt. Die Kopie auf GitHub, die gleich dazukommt, fängt vieles davon ab, aber nicht alles: Mit `git push --force` lässt sich auch die Geschichte dort überschreiben. Lesen Sie deshalb genau, bevor Sie einem Agenten einen Befehl erlauben, der die Geschichte ändert.

## GitHub

Bis hierher liegt die Geschichte nur auf Ihrem Rechner. [GitHub](../Z-anhang/Z010-glossar.md#github) ist ein Dienst im Netz, auf dem Repos liegen. Für Git selbst ist GitHub nicht nötig, für Sie aus zwei Gründen nützlich: Geht der Rechner verloren, ist das Projekt noch da, und Menschen, denen Sie Zugriff geben, können es lesen. GitHub zeigt Markdown-Dateien direkt lesbar an; deshalb ist auch die Beschreibung eines Projekts, die `README.md`, eine Markdown-Datei.

Bevor `git push` etwas nach GitHub schicken kann, muss es dort ein Repo geben. Das Anlegen übernimmt `gh`, das Kommandozeilen-Werkzeug von GitHub. Im Projektordner, nach dem ersten Commit:

```bash
gh repo create lager --private --source=. --remote=origin   # Repo auf GitHub anlegen und verbinden
git push -u origin HEAD                                     # die Commits zum ersten Mal hochladen
```

`lager` ist der Name des Repos auf GitHub. `--private` macht es privat: Nur Sie und Personen, die Sie einladen, können es sehen. Bleiben Sie dabei, solange Sie nicht bewusst etwas veröffentlichen wollen. `--source=.` nennt den aktuellen Ordner als Quelle, `--remote=origin` gibt dem Repo auf GitHub hier den Kurznamen `origin`. `-u origin HEAD` schickt das, woran Sie gerade arbeiten, dorthin und merkt sich das Ziel. Ab dann genügt ein Befehl:

```bash
git push                                   # neue Commits nach GitHub schicken
```

Mit `git clone` holen Sie ein Repo auf einen anderen Rechner.

Im Container von clawbook ist `gh` installiert, und Sie haben sich beim ersten Verbinden bei GitHub angemeldet. `gh repo create` und `git push` kommen deshalb ohne weitere Anmeldung aus. Scheitert es trotzdem am Zugriff, prüft `clawbook github status` die Anmeldung. Außerhalb von clawbook installieren Sie `gh` selbst und melden sich einmal mit `gh auth login` an. Der Projektverwalter `wsm` legt neue Projekte über `gh` auch auf GitHub an, dann entfällt `gh repo create`; ob ein solches Repo privat ist, sehen Sie auf seiner Seite bei GitHub.

## Wie der Agent mit Git umgeht

Alles bisher können Sie dem Agenten überlassen. „Sichere die Arbeit mit Git“ genügt, er kennt die Befehle. Nützlicher ist, wenn er es von selbst tut, und zwar nach festen Regeln. Solche Regeln stehen in einem [Regelwerk](../Z-anhang/Z010-glossar.md#regelwerk), den Dateien, die festlegen, wie ein Agent in einem Projekt arbeitet. Wie ein Regelwerk in ein Projekt kommt, zeigt das Kapitel [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md). Was es für Git festlegt, lässt sich schon jetzt verstehen:

- **Ein Commit je Zug.** Ein Zug ist eine thematisch abgeschlossene Einheit aus mehreren Arbeitsschritten, etwa „Anforderungen überarbeitet“. Der Agent sichert nach jedem Zug, nicht erst am Ende, und bündelt keine drei Züge in einem Commit. So bleibt die Geschichte lesbar und jedes Zwischenergebnis erreichbar.
- **Eine Nachricht mit Präfix.** Jede Commit-Nachricht beginnt mit einem Wort, das sagt, welcher Art die Änderung ist, dann ein Doppelpunkt und die Kurzbeschreibung. In der Geschichte sieht man so auf einen Blick, wo Dokumentation geändert wurde und wo Code.
- **Ein abschließender Commit am Ende der Sitzung.** Was die Züge nicht erfasst haben, sichert der Agent zum Schluss, damit die Sitzung mit einem sauberen Ordner endet.
- **Keine Geheimnisse.** Zugangsdaten, Passwörter und Schlüssel gehören in keine Datei, die in einen Commit kommt. Was einmal in der Geschichte liegt, bleibt dort, auch wenn man es später aus der Datei löscht.
- **Kein Push ohne Anweisung.** Der Agent schickt nichts von sich aus nach GitHub. Was den Rechner verlässt, entscheiden Sie.

## Warum das jetzt zählt

Zurück zur offenen Frage aus dem Kapitel [Die erste Sitzung](A040-die-erste-sitzung.md). Dort hieß es, Accept Edits sei erst sicher, wenn das Projekt unter Git steht, und ein Agent dürfe nur dann ohne Rückfragen arbeiten, wenn der Rechner wegwerfbar und die Arbeit per Git gesichert ist. Jetzt können Sie beides prüfen. Für Accept Edits braucht es ein Repo mit regelmäßigen Commits. Gesichert heißt darüber hinaus: Die Arbeit ist in einem Commit, und der Commit ist auf GitHub. Dann kostet eine zerstörte Datei in der Regel nur die Arbeit seit dem letzten Commit. Eine Garantie ist das nicht, denn ein Agent ohne Rückfragen kann auch die Geschichte beschädigen. Was er außerhalb des Repos anrichtet, an Anmeldungen, an anderen Ordnern, an Ihrem Rechner, kann Git nicht zurückholen. Das ist die erste Bedingung, und sie ist die schwerere.

## Was jetzt klar sein sollte

- Git zeichnet die Geschichte eines Projekts auf, in Commits. Ein Repo ist ein Ordner mit dieser Geschichte.
- Für den Anfang reichen `status`, `add`, `commit`, `log` und `diff`. `git diff` zeigt nicht Vorgemerktes, `git log -p` die Änderungen in den Commits. Zum Zurückgehen `restore` mit seinen Einschränkungen und `checkout` mit der Kennung eines Commits.
- Was nie in einem Commit war, kennt Git nicht. Was in einem Commit ist, liegt gut, aber nicht garantiert sicher: Auch ein Agent kann die Geschichte beschädigen.
- GitHub bewahrt die Geschichte außerhalb Ihres Rechners auf. `gh repo create --private` legt ein privates Repo an, danach schickt `git push` die Commits dorthin.
- Ein Agent sichert nach Regeln: je Zug ein Commit, Nachricht mit Präfix, keine Geheimnisse, kein Push ohne Anweisung.

Damit ist Teil A zu Ende. Sie haben einen laufenden Agenten, wissen, was er ist, warum sein Kontext begrenzt ist, und Ihre Arbeit ist gesichert. Weiter mit [Anforderungen im Gespräch](../B-der-naive-ansatz/B010-anforderungen-im-gespraech.md): Sie bauen mit dem Agenten das erste Programm, auf dem direkten Weg.
