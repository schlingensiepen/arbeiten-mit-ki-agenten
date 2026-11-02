# Sitzungen, die weiterlaufen

> **Stand der Quellen:** [tmux-helper](https://github.com/schlingensiepen/tmux-helper) `v2.0.0`, `README.md`, `docs/Benutzerhandbuch.md`, `docs/LIESMICH.md`.

> **Ist die Verbindung weg, beendet sich die Shell und der Agent stirbt. tmux sorgt dafür, dass er weiterlebt.**

Das Problem zeigt sich meist am ersten Tag. Sie haben in VS Code ein Terminal geöffnet, darin den Agenten gestartet und ihm einen Auftrag gegeben. Dann öffnen Sie über „Open Folder“ einen anderen Ordner, VS Code lädt sein Fenster neu, das Terminal ist weg, und mit ihm der Agent. Dasselbe passiert, wenn die SSH-Verbindung zum Container abbricht oder Sie den Laptop zuklappen. Dieses Kapitel erklärt, warum das so ist, und zeigt dann das Werkzeug, mit dem ein Agent eine getrennte Verbindung überlebt.

## Shell und Prozess

Ein Betriebssystem ist in Schichten gebaut. Innen liegt der Kern, der mit der Hardware spricht. Darüber liegen Schichten, von denen jede nur mit der darunter redet. Die äußerste heißt Schale, englisch Shell. Die grafische Oberfläche ist eine solche Schale, die Kommandozeile eine andere. Die [Shell](../Z-anhang/Z010-glossar.md#shell), um die es hier geht, ist das Programm, das in einem Terminal Ihre Befehle entgegennimmt und ausführt; im Container heißt sie Bash.

Tippen Sie `claude`, startet die Shell den Agenten als eigenen Prozess, also als laufendes Programm, und bleibt sein Elternprozess. Schließt sich das Terminalfenster oder reißt die Verbindung ab, bekommt die Shell das Signal, dass ihr Terminal weg ist, und reicht es an die Programme weiter, die sie gestartet hat. Diese beenden sich daraufhin, wenn sie nichts anderes vorsehen. Für ein Programm, das zwei Sekunden läuft, ist das vernünftig: Niemand soll auf einem Rechner mit vielen Benutzern Prozesse starten und pfeifend weggehen. Für einen Agenten, der zwanzig Minuten an einer Aufgabe arbeitet, ist es unbrauchbar.

Ein Hinweis zum Wort Kontext, falls Sie über Prozesse weiterlesen: Dort meint es den Zustand eines Prozesses, den das Betriebssystem verwaltet. Mit dem Kontextfenster des Modells aus dem Kapitel [Kontext](A020-kontext.md) hat das nichts zu tun.

## tmux

Die Lösung ist ein Prozess, der stehen bleibt und das Terminal festhält, auch wenn Ihr Fenster verschwindet. Genau das tut [tmux](../Z-anhang/Z010-glossar.md#tmux), ein Terminal-Multiplexer: Er betreibt auf dem Rechner eine oder mehrere Terminal-Sitzungen und löst sie vom Fenster, in dem Sie sie gerade sehen. Sie hängen sich an eine Sitzung an, arbeiten, und können sich wieder lösen. Die Sitzung läuft weiter, der Agent darin auch.

Die Befehle, die Sie brauchen, im Terminal des Containers:

```bash
tmux new -s lager        # neue Sitzung mit dem Namen lager, Sie sind gleich drin
tmux ls                  # welche Sitzungen laufen
tmux attach -t lager     # an die Sitzung lager anhängen
tmux attach              # an die zuletzt benutzte Sitzung anhängen
```

Lösen, ohne die Sitzung zu beenden: `Strg+B` drücken, loslassen, dann `d`. Sie sind wieder in der normalen Shell, die Sitzung läuft im Hintergrund weiter. Beenden Sie dagegen den Agenten mit `/exit` und die Shell in der Sitzung mit `exit`, ist die Sitzung zu Ende.

Die Faustregel: Zum Arbeiten mit dem Agenten eine tmux-Sitzung öffnen und den Agenten darin starten. Um später an den laufenden Agenten zu kommen, ein beliebiges Terminal öffnen und `tmux attach`. Ob das Terminal in VS Code liegt, in PowerShell nach `ssh clawbook` oder in einem Tab unter Windows, ist egal; die Sitzung ist dieselbe. Der Projektverwalter `wsm` aus dem Kapitel [Einen Agenten bekommen](A030-einen-agenten-bekommen.md) startet Agenten von sich aus in einer tmux-Sitzung.

Die Grenze: Das hält, solange der Rechner läuft, auf dem tmux läuft. Wird der Container angehalten oder Windows neu gestartet, sind die Sitzungen weg. Auf einem Rechner, der durchläuft, lebt eine Sitzung dagegen beliebig lange.

## Eine Sitzung fortsetzen

Ist der Agent doch beendet worden, weil der Rechner aus war, ist nicht alles verloren. Die meisten Harnesses speichern den Verlauf einer Sitzung auf der Platte und können ihn wieder laden. Claude Code setzt mit dem Schalter `-c` die letzte Sitzung fort, die in diesem Ordner lief (Stand Oktober 2026):

```bash
cd ~/source/sandbox/lager
claude -c
```

Der Agent liest dann den alten Verlauf wieder in den Kontext und macht weiter, als wäre nichts gewesen. Zwei Dinge sollten Sie dazu wissen. Erstens kommt der Verlauf vollständig zurück, mit allem, was das Fenster vorher schon gefüllt hat. Zweitens ist der gespeicherte Verlauf ein Verlauf, kein Ergebnis. Bevor Sie am Abend aufhören, lassen Sie den Agenten das Erreichte in Dateien schreiben, wie im Kapitel Kontext beschrieben. Dann hängt der nächste Tag nicht daran, dass das Fortsetzen klappt.

## Zwei Wege zur laufenden Sitzung

Sie haben jetzt Sitzungen, die weiterlaufen. Bleibt die Frage, wie Sie bequem zu ihnen zurückkommen. Es gibt zwei Wege.

**Das Terminal in VS Code.** Sie öffnen in VS Code ein Terminal und tippen `tmux attach -t lager`. Das ist der kürzeste Weg, wenn Sie ohnehin in VS Code arbeiten. Lädt VS Code sein Fenster neu, ist nur das Terminal weg, nicht die Sitzung; Sie hängen sich wieder an.

**tmux-helper unter Windows.** [tmux-helper](../Z-anhang/Z010-glossar.md#tmux-helper) ist ein Windows-Programm, das die tmux-Sitzungen entfernter Rechner auflistet und als Tabs im Windows Terminal öffnet. Die Anwendung selbst nennt sich Open-TmuxTabs. Sie läuft unter Windows ohne Installation: In PowerShell lädt ein Befehl die ausführbare Datei aus dem neuesten Release und startet sie.

```powershell
irm https://github.com/schlingensiepen/tmux-helper/releases/latest/download/open-tmux-tabs.exe -OutFile "$env:TEMP\open-tmux-tabs.exe"; Start-Process "$env:TEMP\open-tmux-tabs.exe" -Wait
```

Dazu brauchen Sie das Windows Terminal, das ab Windows 11 vorinstalliert ist und sich sonst aus dem Microsoft Store installieren lässt, den OpenSSH-Client von Windows, tmux auf dem entfernten Rechner und einen SSH-Zugang mit Schlüssel. Bei clawbook ist das alles schon da; der Rechner heißt in der SSH-Konfiguration `clawbook`. Beim ersten Start drücken Sie `n`, geben `clawbook` ein und bestätigen. Der Eintrag wird grün, sobald die Verbindung steht, rechts erscheinen die laufenden tmux-Sitzungen. Enter öffnet alle als Tabs im Windows Terminal, je Tab eine SSH-Verbindung mit angehängter Sitzung. Das Programm bleibt danach offen, sodass Sie später weitere Sitzungen auswählen und öffnen können.

![Links ein oranger Block tmux-helper, Open-TmuxTabs, mit einem Pfeil öffnet auf einen Container Windows Terminal, der drei grüne Tabs enthält: lager, done, notizen. Rechts ein Container Entfernter Rechner mit einer Fläche tmux, darin drei blaue Blöcke Sitzung lager, Sitzung done, Sitzung notizen, jeweils mit Agent läuft. Von jedem Tab führt ein Pfeil ssh zur gleichnamigen Sitzung.](bilder/A050-sitzungen.svg)

**Tabs, Sitzungen und entfernter Rechner.** Die Sitzungen und die Agenten darin leben in tmux auf dem entfernten Rechner. Ein Tab im Windows Terminal ist nur eine Verbindung dorthin; geht er zu, läuft die Sitzung weiter. tmux-helper öffnet die Tabs für alle Sitzungen auf einmal.

Für eine einzelne Sitzung ist das Terminal in VS Code schneller. tmux-helper lohnt sich, sobald mehrere Agenten gleichzeitig laufen, etwa wenn Sie später mit `peeragent` weitere Agenten als eigene Prozesse starten; davon handelt das Kapitel [peeragent](../H-mehrere-agenten/H020-peeragent.md). Dann sind drei Sitzungen auf einem Rechner drei Klicks, nicht drei Mal anmelden und anhängen.

## Was jetzt klar sein sollte

- Die Shell startet den Agenten als Kindprozess. Geht das Terminal oder die Verbindung weg, endet die Shell und mit ihr der Agent.
- tmux löst Sitzungen vom Fenster. Agent in einer tmux-Sitzung starten, mit `Strg+B`, `d` lösen, mit `tmux attach` zurückkommen. Das hält, solange der Rechner läuft.
- Eine beendete Sitzung lässt sich oft fortsetzen, in Claude Code mit `claude -c`. Verlassen Sie sich trotzdem auf Dateien, nicht auf den Verlauf.
- Zurück zur Sitzung kommen Sie über das Terminal in VS Code oder, bei mehreren Sitzungen, über tmux-helper unter Windows.

Weiter mit [Git als Gedächtnis](A060-git-als-gedaechtnis.md): wie Dateien nicht nur bleiben, sondern auch ihre Geschichte behalten.
