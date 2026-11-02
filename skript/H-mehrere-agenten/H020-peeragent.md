# peeragent

> **Stand der Quellen:** [peeragent](https://github.com/schlingensiepen/peeragent) `v0.2.0`, `README.md`, `AGENTS.md`, `docs/cli.md`, `docs/install.md`, `examples/quick-start.md`, `examples/task-file-template.md`, `skills/launch-peer-agent/SKILL.md`.

Der Subagent aus dem vorigen Kapitel endet mit seinem Auftrag und berichtet nur dem Agenten, der ihn gestartet hat. Manchmal wollen Sie etwas anderes: einen zweiten Agenten, der stundenlang neben Ihrem arbeitet, in einem eigenen Fenster, in das Sie hineinsehen und in dem Sie mit ihm reden können, während Ihre Sitzung weiterläuft. Im Beispiel DONE arbeitet Ihre Sitzung am Backend und am Wiki; die Kommandozeile könnte parallel entstehen. [peeragent](../Z-anhang/Z010-glossar.md#peeragent) ist ein kleines Kommandozeilen-Werkzeug, das genau das tut: Es startet einen zweiten Agenten als eigenen Prozess in einer eigenen [tmux](../Z-anhang/Z010-glossar.md#tmux)-Sitzung. Dieses Kapitel zeigt, wann ein zweiter Agent der richtige Weg ist, wie der Start abläuft und was der zweite Agent von Ihnen braucht, um arbeiten zu können.

## Subagent oder zweiter Agent?

Beide sind Agenten mit eigenem, frischem Fenster. Der Unterschied liegt darin, wo sie laufen und wie lange.

| | Subagent | Zweiter Agent mit peeragent |
|---|---|---|
| Läuft | in Ihrem Harness, in Ihrer Sitzung | als eigener Prozess in eigener tmux-Sitzung |
| Lebt | bis sein Auftrag erledigt ist | so lange, bis jemand die Sitzung beendet |
| Harness | derselbe wie Ihrer | frei wählbar, auch ein anderer |
| Zusehen | nicht möglich | jederzeit, in seiner Sitzung |
| Berichtet | an den Agenten, der ihn gestartet hat | nur über einen Weg, den der Auftrag beschreibt |

Als Faustregel: Ein kurzer, klar umrissener Schritt, dessen Ergebnis Sie jetzt brauchen, geht an einen Subagenten. Parallele Arbeit, die länger dauert, ein eigenes Fenster braucht und für Sie erreichbar bleiben soll, geht an einen zweiten Agenten.

Der Name sagt, wofür das Werkzeug gedacht ist: ein Agent, der neben Ihrem arbeitet, englisch peer, im eigenen Prozess und mit eigenem Kontext. Die Dokumentation von peeragent ist dabei genau: Was das Werkzeug startet, ist zunächst nur ein Harness in einem Terminalfenster. Es hat keinen Namen in einem Team und kein Postfach. Ob daraus ein Mitglied einer Gruppe von Agenten wird, entscheidet sich außerhalb des Werkzeugs, im nächsten Kapitel.

## Was peeragent tut

peeragent startet einen Harness in einer tmux-Sitzung, wartet kurz, liest den ersten Bildschirm und meldet in fester Form zurück, was dort zu sehen ist: ob der Harness bereit ist, arbeitet oder auf eine Antwort wartet, etwa auf die [Vertrauensabfrage](../Z-anhang/Z010-glossar.md#vertrauensabfrage) zum Ordner oder auf eine Anmeldung. Einen Startprompt, der nicht zugestellt werden konnte, reicht es mit einem zweiten Befehl nach. Außerdem listet es, welche Harnesses auf dem Rechner installiert sind.

Es braucht Linux oder WSL2 unter Windows, tmux ab Version 3.2 und Python ab 3.11; eine Variante in Bash liegt bei. Es kennt die Harnesses `claude`, `codex`, `agy`, `opencode` und `copilot` und startet sie, installiert oder konfiguriert sie aber nicht (Stand Oktober 2026). Die Version 0.2.0 ist eine Vorabversion. Vollständig auf dem Harness selbst geprüft ist nur der Weg mit `claude`; was für die anderen getestet ist und was nur aus deren Dokumentation stammt, steht in der Datei `MATURITY.md` des Repos. Lesen Sie sie, bevor Sie sich auf eine Aussage verlassen.

Wer peeragent aufruft, ist offen: Sie selbst im Terminal, oder Ihr Agent, wenn Sie ihn darum bitten. Das Werkzeug ist für den zweiten Fall gebaut. Seine Ausgabe gibt es als Zeilen für Menschen und mit `--json` in einer Form, die ein Agent sicher lesen kann, und ein [Skill](../Z-anhang/Z010-glossar.md#skill) namens `launch-peer-agent` liegt bei, der dem Agenten die Pflichten beibringt, die weiter unten stehen.

Die Installation:

```bash
git clone https://github.com/schlingensiepen/peeragent.git
mkdir -p ~/.claude/skills ~/.local/bin
install -m 0755 peeragent/tools/peeragent.py ~/.local/bin/peeragent
command -v peeragent
```

Die Zeile mit `mkdir -p` legt zwei Ordner an, die auf einem frischen Rechner fehlen können; ohne sie gehen die Installation hier und das Kopieren des Skills weiter unten schief. Die letzte Zeile zeigt, wo die Shell das Programm findet. Bleibt die Antwort leer, steht `~/.local/bin` noch nicht im Suchpfad der Shell; das ist je nach Linux-Distribution verschieden. Dann tragen Sie den Ordner in die Startdatei Ihrer Shell ein, in der bash so, in der zsh ebenso mit `~/.zshrc`:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Dann die erste Probe:

```bash
peeragent version
peeragent list harness
```

Die letzte Zeile zeigt je Harness, ob er gefunden wurde und in welcher Version. Für Claude Code kommt der Skill in den Skill-Ordner:

```bash
cp -r peeragent/skills/launch-peer-agent ~/.claude/skills/
```

Andere Harnesses bekommen den Pfad zur Datei `SKILL.md` genannt und lesen sie als Text.

## Der Auftrag liegt in einer Datei

Dasselbe Prinzip wie beim Subagenten, nur strenger. Der zweite Agent weiß nichts von Ihrem Projekt, Ihrer Sitzung und Ihnen. Alles, was er braucht, steht in einer Auftragsdatei in seinem Arbeitsverzeichnis. Der Prompt, den er beim Start bekommt, zeigt nur darauf. peeragent erzwingt das: Ein Startprompt über 120 Zeichen wird abgewiesen, bevor irgendetwas startet. Absolute Pfade zählen dabei nicht mit, der Zeiger auf die Datei kostet also nichts.

Die Gründe sind handfest. Der Harness bekommt den Prompt als Argument auf der Befehlszeile, wo ihn jeder Benutzer des Rechners in der Prozessliste lesen kann. Ein langer Prompt ist außerdem aus dem Blick, sobald der Bildschirm weitergescrollt ist. Eine Datei dagegen lässt sich versionieren, erneut lesen und beim nächsten Start wieder verwenden.

Die Vorlage für die Auftragsdatei hat fünf Abschnitte, und jeder steht dort, weil ohne ihn ein gestarteter Agent schon einmal schiefgegangen ist:

1. **So erreichst du mich.** Der zweite Agent hat keine Verbindung zu Ihnen. Wenn Sie von ihm hören wollen, beschreibt der Auftrag den Weg: welches Verfahren, welche Adresse. Der einfachste Weg ist ein Ordner, auf den sich beide Seiten einigen, mit festen Dateinamen für jede Richtung. Der zweite Weg ist der Dienst aus dem nächsten Kapitel. Geheimnisse wie Zugangsschlüssel gehören nicht in die Auftragsdatei; sie liegen in einer Datei außerhalb jedes Repos, und der Auftrag nennt nur den Pfad.
2. **Meldung nach dem Einrichten.** Ein Satz wie: Wenn die Schritte unter Einrichten erledigt sind, melde dich über den Weg oben, bevor du mit der Arbeit beginnst. Ohne diese Meldung können Sie einen Agenten, der arbeitet, nicht von einem unterscheiden, der an einer Frage hängt, die Sie nie gesehen haben.
3. **Einrichten.** Was eine frische Sitzung in diesem Projekt sonst tut: Umgebung aktivieren, Abhängigkeiten installieren, die Instruktionsdatei lesen, Tests laufen lassen. Dazu, was zu tun ist, wenn ein Schritt scheitert, besonders wenn die Tests schon vor der Änderung nicht grün sind. Sonst verbringt der Agent seinen Lauf damit, etwas Fremdes zu reparieren.
4. **Die Arbeit.** Was zu ändern oder herzustellen ist, genau genug, dass man es prüfen kann.
5. **Umfang und Ende.** Was diesmal dazugehört und was ausdrücklich nicht, wann der Agent aufhört und was er dann meldet. Eine einzige Abbruchbedingung; bei mehreren nimmt ein Agent die lockerste.

Dazu kommt die Angabe, wo Sie selbst sind: Rechner, Benutzerkonto, Verzeichnis. Dateien in beide Richtungen brauchen alle drei.

## Vorbereiten, Schritt für Schritt

Im Beispiel DONE braucht der zweite Agent drei Dinge: ein eigenes Arbeitsverzeichnis, die Auftragsdatei und den Startprompt. Alle Pfade liegen in Ihrem Home-Verzeichnis. Dieses Beispiel nimmt an, dass Ihr Projekt DONE in `~/source/sandbox/done` liegt; liegt es anderswo, ändern Sie den Pfad im Auftrag.

**Schritt 1: Ordner anlegen.** `done-cli` ist das Arbeitsverzeichnis der Kommandozeile, `austausch/done-cli` der Ordner, in dem Sie und der zweite Agent einander schreiben. Er liegt außerhalb des Projekts.

```bash
mkdir -p ~/source/sandbox/done-cli ~/austausch/done-cli
```

**Schritt 2: Auftragsdatei schreiben.** Der Befehl `cat > Datei <<EOF` schreibt alle folgenden Zeilen bis zur Zeile `EOF` in die Datei. `$HOME` ersetzt die Shell dabei durch den vollen Pfad Ihres Home-Verzeichnisses. So stehen in der Datei absolute Pfade, also Pfade, die mit `/` beginnen. Sie gelten von jedem Verzeichnis aus, und im Startprompt kosten nur sie keine Zeichen. Die Tilde `~` beginnt nicht mit `/` und zählt dort mit.

```bash
cat > ~/source/sandbox/done-cli/AUFTRAG.md <<EOF
# Auftrag: Kommandozeile für DONE bauen

## So erreichst du mich
Ordner $HOME/austausch/done-cli/. Du schreibst status.md und
überschreibst sie bei jeder Meldung. Ich schreibe antwort.md.
Ich lese alle dreißig Minuten.

## Meldung nach dem Einrichten
Wenn die Schritte unter Einrichten erledigt sind, schreibe die
Zeile BEREIT nach status.md, bevor du mit der Arbeit beginnst.
Nenne dabei das Verzeichnis, in dem du dich tatsächlich befindest.
Es soll $HOME/source/sandbox/done-cli sein.

## Einrichten
- Lies die Instruktionsdatei von DONE in
  $HOME/source/sandbox/done/. Ändere dort nichts.
- Gibt es in deinem Verzeichnis schon Tests, lass sie laufen.
  Sind sie nicht grün, melde das und stoppe.

## Die Arbeit
Baue die Kommandozeile für DONE nach dem freigegebenen
Freigabedokument der ersten Marke in
$HOME/source/sandbox/done/output/. Die Schnittstelle zum Backend
steht dort; ändere sie nicht.

## Umfang und Ende
Nur die Kommandozeile, nichts am Backend. Stoppe, wenn alle Tests
grün sind, und melde das in status.md.
EOF
```

**Schritt 3: Startprompt schreiben.** Er kommt in eine eigene Datei neben dem Auftrag:

```bash
cat > ~/source/sandbox/done-cli/.peeragent-prompt.txt <<EOF
Lies $HOME/source/sandbox/done-cli/AUFTRAG.md und führe den Auftrag aus. Nur die Kommandozeile, dann stoppen und in $HOME/austausch/done-cli/status.md melden.
EOF
```

Ohne die beiden Pfade sind das rund achtzig Zeichen, weit innerhalb der Grenze.

## Der Start und der erste Bildschirm

```bash
peeragent start agent --folder ~/source/sandbox/done-cli --harness claude --prompt-file ~/source/sandbox/done-cli/.peeragent-prompt.txt
```

`--folder` ist das Arbeitsverzeichnis des zweiten Agenten, und es ist keine Nebensache. Der gestartete Harness erbt nichts vom Aufrufer, weder dessen aktuelles Verzeichnis noch den Ort der Prompt-Datei. Von diesem Pfad hängt ab, was der Agent sieht, worauf sich seine Vertrauensabfrage bezieht, wo sein Gesprächsverlauf gespeichert wird und wie die tmux-Sitzung heißt. Nennen Sie das Projektverzeichnis selbst, nie den Ordner darüber: Dann meldet nichts einen Fehler, aber alles sitzt eine Ebene zu hoch.

peeragent legt die Sitzung an, sie heißt `peeragent-<Ordnername>-<Harness>-<acht Zeichen>`, hier also etwa `peeragent-done-cli-claude-1a2b3c4d`. Nach einer kurzen Wartezeit liest es den Bildschirm und ordnet ihn ein. Der erste Start in einem neuen Verzeichnis endet fast immer mit einer Frage, das ist kein Fehler:

| Einordnung | Bedeutung | Was Sie tun |
|---|---|---|
| `ready` | Der Harness wartet auf Eingabe. Der Prompt ist angekommen. | Nichts. |
| `busy` | Der Harness arbeitet. | Warten, in die Sitzung sehen. Den Prompt nicht noch einmal schicken. |
| `trust_prompt` | Vertrauensabfrage zum Ordner. | Mit der gemeldeten Tastenfolge antworten, siehe unten. |
| `auth_prompt` | Der Harness ist nicht angemeldet. | Die Anmeldung ist Handarbeit außerhalb von peeragent. |
| `provider_prompt` | Dem Harness fehlt ein Modellanbieter. | Ebenfalls Handarbeit im Harness. |
| `unknown` | Kein bekanntes Muster. | Den Bildschirm ansehen und selbst entscheiden. Nichts raten. |

Die Vertrauensabfrage beantwortet peeragent nicht selbst. Es meldet die Tastenfolge, die sie bestätigt, und Sie schicken sie in die Sitzung. Für `claude` sind das zwei Tasten, weil der Dialog die ablehnende Antwort vorauswählt; der Doppelpunkt am Ende des Ziels ist Pflicht:

```bash
tmux send-keys -t "=peeragent-done-cli-claude-1a2b3c4d:" Down Enter
```

Diese Tastenfolgen beschreiben die Dialoge eines bestimmten Tages. Eine neue Version des Harness kann sie umbauen. Sieht der Bildschirm anders aus als beschrieben, schicken Sie nichts, sondern sehen in die Sitzung. Das gilt erst recht bei `unknown`: Ein Harness kann beim Start anbieten, sich selbst zu aktualisieren, und die Ziffer, die in einem Dialog „ja, ich vertraue dem Ordner“ heißt, löst in einem anderen eine Installation aus.

Danach prüfen Sie, ob der Prompt angekommen ist, indem Sie den Bildschirm lesen:

```bash
tmux capture-pane -t "=peeragent-done-cli-claude-1a2b3c4d:" -p
```

Steht der Prompt dort und arbeitet der Harness, sind Sie fertig. Nur wenn die Eingabezeile leer ist und der Prompt nirgends zu sehen, wurde er nicht übernommen. Dann, und nur dann, reichen Sie ihn nach:

```bash
peeragent send --session peeragent-done-cli-claude-1a2b3c4d --prompt-file ~/source/sandbox/done-cli/.peeragent-prompt.txt
```

Ein zweimal zugestellter Prompt heißt: Der Auftrag wird zweimal ausgeführt. peeragent meldet ausdrücklich, wenn ein Prompt nicht zugestellt wurde; `send` gehört nur hinter diese Meldung.

## Danach: der Agent lebt allein

peeragent kehrt zurück, sobald es den ersten Bildschirm gemeldet hat. Der zweite Agent läuft in seiner tmux-Sitzung weiter, unbeaufsichtigt, und überlebt den Aufruf. Das ist der Zweck des Werkzeugs, und es ist der Teil, der überrascht: Zwischen dem Aufrufer und dem Agenten besteht keine Verbindung mehr. Nichts meldet sich von allein zurück.

Was bleibt, ist der Name der Sitzung. Er ist die eine Sache, die man sich merken muss, und ein Agent, der peeragent benutzt, ist verpflichtet, ihn der Person zu nennen, für die er arbeitet. Mit dem Namen sehen Sie zu, ohne versehentlich etwas einzutippen:

```bash
tmux attach -r -t "=peeragent-done-cli-claude-1a2b3c4d"
```

Ohne `-r` sind Sie in der Sitzung wie in jeder anderen aus dem Kapitel [Sitzungen, die weiterlaufen](../A-verstehen-und-loslegen/A050-sitzungen-die-weiterlaufen.md): Sie lesen mit und können dem zweiten Agenten selbst schreiben. Deshalb bleibt er für Sie erreichbar. Unter Windows listet der dort beschriebene [tmux-helper](../Z-anhang/Z010-glossar.md#tmux-helper) alle Sitzungen eines Rechners und öffnet sie als Tabs; mit mehreren Agenten lohnt er sich besonders.

Der Weg zurück zum ersten Agenten ist damit noch nicht da. Das Zusehen ist kein Gespräch. Wer von dem zweiten Agenten hören will, richtet einen Weg ein und beschreibt ihn im Auftrag, wie oben. Was der zweite Agent liefert, erscheint dort, wohin die Auftragsdatei ihn geschickt hat, und im Git-Status seines Verzeichnisses, nicht in der Ausgabe von peeragent.

Einige Regeln aus der Dokumentation, die sich bewährt haben:

- **Führen Sie Buch.** Wer mehrere Agenten startet, schreibt nach jedem Start eine Zeile in eine eigene Datei: Sitzungsname, Harness, Verzeichnis, Uhrzeit, Auftrag. `tmux ls` zeigt die Sitzungen, aber nicht, wer was tut.
- **Sehen Sie in festem Takt nach**, etwa alle dreißig bis sechzig Sekunden, bis die erste Meldung da ist. Eine Sitzung, die auf eine Antwort wartet, sieht aus wie eine, die schläft. Legen Sie vorher fest, nach wie langer Zeit ohne Meldung der Agent als nicht arbeitend gilt.
- **Entscheiden Sie je Frage, raten Sie keine Taste.** Ein laufender Agent kann jederzeit an einer Rückfrage halten. Eine Option, die seine Rechte für den Rest der Sitzung erweitert, wählen Sie nur, wenn Sie das wirklich wollen.
- **Rückfragen abschalten ist Ihre Entscheidung.** Jeder Harness hat einen Schalter, der Werkzeugaufrufe ohne Nachfrage erlaubt. Ein Agent, der peeragent bedient, darf diesen Schalter nicht von sich aus setzen; er fragt Sie vorher, mit Harness, Verzeichnis und Auftrag. Was dieser Schalter bedeutet, steht im Kapitel [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md).
- **peeragent beendet nie eine Sitzung.** Aufräumen ist Ihre Sache, eine Sitzung nach der anderen, mit vollem Namen und dem Gleichheitszeichen davor, damit tmux keinen Namen mit gleichem Anfang trifft: `tmux kill-session -t "=peeragent-done-cli-claude-1a2b3c4d"`. Niemals `tmux kill-server`: Der tmux-Server trägt alle Ihre Sitzungen, die eigenen, die anderer Agenten und frühere Läufe.

## Ohne peeragent

Einen Harness in einer tmux-Sitzung können Sie auch von Hand starten:

```bash
tmux new-session -d -s done-cli -c ~/source/sandbox/done-cli claude
```

peeragent lohnt sich, wenn Sie die einheitliche, maschinenlesbare Meldung über den ersten Bildschirm, seine Einordnung und das Protokoll je Aufruf wollen, also vor allem dann, wenn ein Agent den zweiten startet. Die Pflichten von oben, Auftragsdatei, Meldung nach dem Einrichten, Sitzungsname an den Menschen, gelten so oder so.

## Was jetzt klar sein sollte

- Ein zweiter Agent ist ein eigener Prozess in eigener tmux-Sitzung. Er läuft parallel, überlebt Ihren Aufruf, und Sie können ihm zusehen und mit ihm reden.
- Sein Auftrag ist eine Datei im Arbeitsverzeichnis, der Startprompt nur ein Zeiger darauf. Die Datei beschreibt den Weg, auf dem er sich meldet, die Meldung nach dem Einrichten, die Einrichtungsschritte, die Arbeit und das Ende.
- Der erste Bildschirm endet meist mit einer Frage. peeragent ordnet sie ein und nennt die Antwort, schickt sie aber nicht selbst. Bei Unbekanntem wird hingesehen, nicht geraten.
- Nach dem Start besteht keine Verbindung mehr. Der Sitzungsname ist das, was bleibt; er gehört immer zum Menschen.

Weiter mit [simple-a2a](H030-simple-a2a.md): Wie Agenten einander Nachrichten schicken, zuerst als Dateien, dann über einen kleinen Dienst.
