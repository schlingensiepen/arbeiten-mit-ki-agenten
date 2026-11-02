# Arbeiten mit KI-Agenten

Ein Skript für Studierende des ersten Semesters ohne Vorkenntnisse: wie man mit KI-Agenten arbeitet, warum ein Gespräch allein nicht trägt, und wie eine Arbeitsweise aussieht, die über Wochen, viele Sitzungen und mehrere Versionen hält. Es erklärt die Werkzeuge, die dazu gehören, und begründet, warum sie so gebaut sind, wie sie gebaut sind.

Das Skript steht unter `skript/`, je Teil ein Ordner mit einem README und den Kapiteln. Es ist aus einer Werkstatt abgeleitet; jedes Kapitel nennt oben, aus welchen öffentlichen Quellen und welchem Stand es stammt. Was nur für heute gilt, trägt einen Stand, etwa „Stand Oktober 2026“.

## Für wen

Für Studierende im ersten Semester, die noch keinen Agenten benutzt, noch kein Programm geschrieben und noch kein Projekt geführt haben. Fachstoff kommt nur als Beispiel vor: eine Lagerverwaltung in den ersten Teilen, die Aufgabenverwaltung DONE ab dem Aufsetzen eines Projekts. Wer schon mit Agenten arbeitet, findet in den Teilen D bis H die Arbeitsweise und im Anhang die Begriffe.

## Wie man es liest

Die Teile A bis H bilden die Lesekette und bauen aufeinander auf. Erst tun, dann begründen: Teil A führt zu einem laufenden Agenten, Teil B baut damit etwas auf dem naiven Weg, Teil C begründet daraus, was eine Arbeitsweise leisten muss, und die Teile D bis H lösen das ein. Erst Teil H nimmt weitere Agenten hinzu.

1. [Teil A: Verstehen und loslegen](skript/A-verstehen-und-loslegen/README.md). Was ein Agent ist, warum sein Kontext begrenzt ist, und Schritt für Schritt bis zum laufenden Agenten mit Git als Gedächtnis.
2. [Teil B: Der naive Ansatz](skript/B-der-naive-ansatz/README.md). Eine Lagerverwaltung auf dem direkten Weg von den Anforderungen zum Programm, und die Stelle, an der dieser Weg bricht.
3. [Teil C: Der langfristige Ansatz](skript/C-der-langfristige-ansatz/README.md). Warum der naive Ansatz scheitert und was eine Arbeitsweise leisten muss, die trägt.
4. [Teil D: Wissen im Wiki](skript/D-wissen-im-wiki/README.md). Das Wiki als Quelle der Wahrheit, das Regelwerk, der Sessionstart, das Aufsetzen eines Projekts und die Register.
5. [Teil E: Mensch und Agent](skript/E-mensch-und-agent/README.md). Wer was entscheidet, wie der Agent Klärpunkte vorlegt und wie eine Sitzung sauber endet.
6. [Teil F: Marken und Freigaben](skript/F-marken-und-freigaben/README.md). Die Marke als benanntes Ergebnis, das Freigabedokument als Sammler und Freezer, die Freigabe für einen Zweck.
7. [Teil G: Der Gesamtprozess](skript/G-der-gesamtprozess/README.md). Phasen und Prüfkette, wer prüft und warum ein zweites Modell darauf schaut, Werkstatt und Produkt, Sonderwege für bestehende Projekte.
8. [Teil H: Mehrere Agenten](skript/H-mehrere-agenten/README.md). Subagenten, ein zweiter Agent als eigener Prozess, Nachrichten zwischen Agenten und das Zusammenspiel.

Drei Teile stehen außerhalb der Lesekette. Die Kapitel verweisen an der passenden Stelle dorthin.

- [Teil X: Hintergrund](skript/X-hintergrund/README.md) erklärt, was hinter einem Begriff oder einer Regel steckt: wie Maschinen lernen, was Modellieren heißt, was Aufpasser-Modelle sind. Die Lesekette bleibt ohne ihn vollständig lesbar.
- [Teil Y: Beispiele](skript/Y-beispiele/README.md) enthält die Startprompts der beiden Beispiele, die das Skript tragen, zum Nachmachen und zum Lesen.
- [Teil Z: Anhang](skript/Z-anhang/README.md) enthält das Glossar. Jedes Kapitel verlinkt einen Fachbegriff beim ersten Auftreten dorthin.

Jedes Kapitel ist für sich lesbar, beginnt mit dem Stand seiner Quellen und endet mit dem, was danach klar sein sollte, und dem Link zum nächsten Kapitel. Befehle stehen als kopierbare Codeblöcke.

## Behandelte Werkzeuge

Das Skript erklärt die folgenden Werkzeuge und zeigt sie am Beispiel. Es empfiehlt keines; was ein Werkzeug kann und wo seine Grenze liegt, steht im jeweiligen Kapitel.

- [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung): die Vorlage für Projekte mit vorbereitetem Wiki, Regelwerk und Anleitungen für neues Projekt, Migration und Upgrade (Teile D bis G).
- [clawbook-lehre](https://github.com/schlingensiepen/clawbook-lehre): ein fertig eingerichteter Arbeitsrechner für die Arbeit mit Agenten als Container-Image (Teil A).
- [tmux-helper](https://github.com/schlingensiepen/tmux-helper): ein Windows-Programm, das tmux-Sitzungen entfernter Rechner auflistet und als Tabs öffnet (Teil A).
- [peeragent](https://github.com/schlingensiepen/peeragent): startet einen zweiten Agenten als eigenen Prozess in einer tmux-Sitzung (Teil H).
- [simple-a2a](https://github.com/schlingensiepen/simple-a2a): ein kleines Protokoll und ein Dienst, mit dem Agenten einander Nachrichten schicken (Teil H).
- [skill-a2a](https://github.com/schlingensiepen/skill-a2a): der einfache Weg dazu, Nachrichten als Dateien auf demselben Rechner, als Skill für den Agenten (Teil H).

## Lizenz

Inhalt unter CC BY 4.0, Attribution: Jörn Schlingensiepen,
`https://github.com/schlingensiepen/arbeiten-mit-ki-agenten`. Quelltext unter
Apache-2.0 (Ordner `tools/`). Details: [`LICENSE`](LICENSE).
