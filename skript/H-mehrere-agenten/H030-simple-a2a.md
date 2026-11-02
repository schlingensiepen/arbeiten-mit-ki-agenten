# simple-a2a

> **Stand der Quellen:** [skill-a2a](https://github.com/schlingensiepen/skill-a2a) `v1.0.1`, `README.md`, `AGENTS.md`, `skills/a2a/SKILL.md`, `skills/a2a/invitation.md`; [simple-a2a](https://github.com/schlingensiepen/simple-a2a) `v0.1.1`, `README.md`, `docs/quick-start.md`, `mcp/README.md`, `src/simple_a2a/describe/texts/messaging/guide.md`, `src/simple_a2a/describe/texts/admin/realms.md`.

Zwei Agenten aus dem vorigen Kapitel laufen nebeneinander, aber keiner weiß vom anderen. Im Beispiel DONE müssen der Agent des Backends und der Agent der Kommandozeile die Schnittstelle abstimmen: welche Befehle es gibt, welche Daten hin- und hergehen. Wenn Sie das selbst übertragen, aus dem einen Fenster kopieren und in das andere einfügen, kostet das Ihre Zeit und Ihr Fenster. Dass Agenten miteinander reden, ist wieder ein Mechanismus, das eigene Fenster zu schonen. Dieses Kapitel zeigt, wie Agenten einander Nachrichten schicken. Zuerst die Wörter, dann der einfache Weg mit Nachrichten als Dateien, dann seine Grenze, und schließlich der kleine Dienst [simple-a2a](../Z-anhang/Z010-glossar.md#simple-a2a), der diese Grenze aufhebt.

## Nachrichten statt Zuruf

Ein Agent ist zwischen zwei Prompts nicht erreichbar. Er wartet auf Eingabe, und ein Zuruf von außen erreicht ihn nicht. Deshalb reden Agenten nicht wie am Telefon, sondern wie per Post: Eine Nachricht ist ein Text, der im Postfach des Empfängers liegt, bis dieser hineinsieht. Der Absender wartet nicht, der Empfänger liest, wenn er dran ist. Drei Wörter reichen für das Ganze:

- Ein [Team](../Z-anhang/Z010-glossar.md#team) ist eine Gruppe von Agenten, die einander schreiben. Es hat einen Namen, und jeder Agent darin hat einen Namen.
- Ein [Postfach](../Z-anhang/Z010-glossar.md#postfach), englisch Inbox, ist der Eingang, in dem die Nachrichten für einen Agenten liegen. Je Team hat jeder Agent genau eines.
- Ein [Realm](../Z-anhang/Z010-glossar.md#realm) ist der abgegrenzte Bereich, in dem Teams und Agenten zusammenarbeiten. Ihn gibt es erst beim Dienst; auf dem einfachen Weg genügen Team und Postfach.

## Der einfache Weg: Nachrichten als Dateien

Der einfache Weg heißt skill-a2a. Das ist ein [Skill](../Z-anhang/Z010-glossar.md#skill), also eine Anleitung, die der Agent bei Bedarf in sein Fenster lädt. Er bringt Agenten, die auf demselben Rechner unter demselben Benutzerkonto laufen, bei, einander Nachrichten als Dateien zu schicken. Kein Dienst, kein Port, nichts zu installieren außer dem Skill selbst. Und er funktioniert über die Grenzen der Harnesses hinweg: Der eine Agent kann in Claude Code laufen, der andere in Codex, solange beide den Skill gelesen haben.

Das Postfach ist ein Verzeichnis, das nur der eigene Benutzer lesen darf. Eine Nachricht ist eine Datei, die der Absender direkt in das Postfach des Empfängers legt. Was im Postfach liegt, ist unerledigt; der Empfänger löscht eine Nachricht, sobald er sie bearbeitet hat. Es gibt keinen Ausgang, kein Archiv und keine Weiterleitung. Der Skill kennt zwei Spielarten: zentral, mit einem gemeinsamen Verzeichnis je Team, etwa `~/.a2a/<team>/`, in dem jeder Agent sein Postfach unter seinem Namen hat; und dezentral, mit dem Postfach im eigenen Arbeitsverzeichnis jedes Agenten. Der Skill bietet beide an, dazu den Dienst von weiter unten als dritte, und sagt, was jede kostet. Sie wählen und vergeben die Namen.

Eine Nachricht ist eine Markdown-Datei mit einem Kopf, einer Leerzeile und dem Text:

```text
From: backend
To: cli
Date: 2026-11-01T14:21:29.151Z
Subject: Schnittstelle Aufgabe anlegen

Vorschlag: Der Befehl heißt "done add". Er nimmt einen Titel
und wahlweise ein Datum. Das Backend liefert die neue Nummer
zurück. Passt das zu deinem Entwurf?
```

Der Dateiname beginnt mit dem Zeitstempel, dann Absender und Betreff, damit die Dateien nach Zeit sortieren und jede eindeutig ist. Eine Antwort nennt im Kopf unter `In-Reply-To` den Dateinamen der Nachricht, auf die sie antwortet. Der Skill bringt zwei kleine Skripte mit: `a2a-send` legt eine Nachricht so ab, dass sie entweder ganz oder gar nicht im Postfach erscheint, und `a2a-watch` wartet im Hintergrund, bis im Postfach etwas liegt.

Das Warten ist der eigentliche Trick. Weil niemand in die Sitzung des Agenten tippt, um ihn zu wecken, stellt sich der Agent selbst einen Wecker, mit den Mitteln, die sein Harness bietet. `a2a-watch` läuft als Hintergrundbefehl und endet, sobald eine Nachricht da ist oder eine Frist abläuft. Danach liest der Agent sein Postfach in der Reihenfolge der Dateinamen, bearbeitet jede Nachricht, löscht sie und stellt den Wecker neu. Nach einer Komprimierung seines Fensters sieht er ebenfalls zuerst ins Postfach.

Wie kommt der zweite Agent ins Team? Der erste lädt ihn ein. Der Skill liefert dafür eine Vorlage für den Einladungs-Prompt: Spielart, Team, Name des Eingeladenen und des Einladenden, Ort des Postfachs, wie er geweckt wird, was Sie erlaubt haben, und die Bitte um eine erste Nachricht, damit beide wissen, dass der Weg funktioniert. Diese Einladung ist genau das, was im vorigen Kapitel unter „So erreichst du mich“ in die Auftragsdatei gehört. Wie der zweite Agent gestartet wird, ist Ihre Sache; peeragent ist ein Weg.

Drei Regeln gelten immer. Ein Agent legt nie das Postfach eines anderen an; fehlt es, schlägt das Senden fehl. In fremden Postfächern darf er nur auflisten und Neues hinzufügen, nie fremde Nachrichten lesen, ändern oder löschen. Und in Nachrichten stehen keine Geheimnisse, keine Schlüssel und keine Passwörter. Dass ein Agent in ein fremdes Verzeichnis schreiben darf, ist Ihre Erlaubnis: zentral einmal für das gemeinsame Verzeichnis, dezentral einmal je fremdem Postfach.

## Beispiel DONE: die Schnittstelle abstimmen

Ihre Sitzung arbeitet am Backend, ein zweiter Agent soll an der Kommandozeile arbeiten. Die Reihenfolge zählt: erst der Skill, dann die Einladung, zuletzt der Start des zweiten Agenten. Er bekommt die Einladung mit seinem Auftrag; was erst nach seinem Start dort steht, sagt ihm niemand.

Im vorigen Kapitel haben Sie diesen Agenten schon gestartet, mit der Meldung über `status.md`. Dieser Lauf kennt kein Postfach, und eine geänderte Auftragsdatei erreicht ihn nicht. Darum geht es in vier Schritten: Skill installieren, den alten Lauf beenden, Auftrag und Startprompt auf das Postfach umstellen, neu starten.

**Schritt 1: Skill installieren lassen.** Das Repo enthält mit der Datei `AGENTS.md` eine Anleitung für den Agenten selbst, und seine README nennt diesen Weg zuerst. Sie brauchen nur einen Prompt:

```text
Lade den Skill von github.com/schlingensiepen/skill-a2a und installiere ihn für alle deine Projekte.
```

Der Agent holt das Repo, kopiert das Verzeichnis `skills/a2a/` dorthin, wo sein Harness nach Skills sucht, für Claude Code also nach `~/.claude/skills/a2a/`, macht die Skripte ausführbar und lässt die Tests des Repos laufen. Sie enden mit `… passed, 0 failed`. „Für alle deine Projekte“ steht im Prompt, weil die Anleitung ihn sonst danach fragen lässt, bevor er an einen Ort installiert, der für alle Ihre Projekte gilt. Hier ist das richtig: Der zweite Agent arbeitet in einem anderen Verzeichnis. Beide laufen unter demselben Benutzerkonto, einmal genügt also. Ein Harness ohne Skills legt das Verzeichnis an einen Ort, den er wiederfindet, und bekommt den Pfad zur Datei `SKILL.md` in seiner Instruktionsdatei genannt.

Von Hand geht es so; die letzte Zeile macht die Skripte ausführbar:

```bash
git clone https://github.com/schlingensiepen/skill-a2a.git
mkdir -p ~/.claude/skills
cp -R skill-a2a/skills/a2a ~/.claude/skills/a2a
chmod 755 ~/.claude/skills/a2a/scripts/a2a-send ~/.claude/skills/a2a/scripts/a2a-watch
```

Für eine neue Version löschen Sie vorher das alte Verzeichnis, sonst legt `cp -R` das neue als `a2a/a2a` hinein.

**Schritt 2: Den alten Lauf beenden.** peeragent beendet nie eine Sitzung, das tun Sie, mit dem Namen Ihrer Sitzung statt des Beispiels. `tmux ls` zeigt ihn. Haben Sie den Agenten im vorigen Kapitel nicht gestartet, entfällt dieser Schritt.

```bash
tmux kill-session -t "=peeragent-done-cli-claude-1a2b3c4d"
```

Was der Lauf im Verzeichnis `done-cli` geschrieben hat, bleibt liegen.

**Schritt 3: Auftrag und Startprompt umstellen lassen.** Sie sagen dem ersten Agenten:

```text
Richte mit dem Skill a2a ein Team done ein, zentral unter ~/.a2a/done/. Dein Name ist backend. Ihr dürft beide in dieses Verzeichnis schreiben. Lade den Agenten cli ein; seine Einladung ersetzt den Inhalt des Abschnitts „So erreichst du mich“ der Datei ~/source/sandbox/done-cli/AUFTRAG.md. Stelle in dieser Datei auch die Abschnitte „Meldung nach dem Einrichten“ und „Umfang und Ende“ von status.md auf eine Nachricht an backend um. Ersetze in ~/source/sandbox/done-cli/.peeragent-prompt.txt den Schluss „in …/status.md melden“ durch „an backend melden“.
```

Der erste Agent legt sein Postfach an, schreibt die Einladung in die Auftragsdatei, die Sie im vorigen Kapitel vorbereitet haben, und ändert die Meldewege. Die Meldung nach dem Einrichten und die am Ende gehen jetzt als Nachricht an `backend`. Sie selbst haben kein Postfach, Sie erfahren beides in Ihrer Sitzung vom ersten Agenten. Prüfen Sie die Umstellung, bevor Sie starten:

```bash
grep -n status.md ~/source/sandbox/done-cli/AUFTRAG.md ~/source/sandbox/done-cli/.peeragent-prompt.txt
```

Keine Ausgabe heißt: Beide Dateien sind umgestellt.

**Schritt 4: Zweiten Agenten neu starten.** Der Befehl ist derselbe wie im vorigen Kapitel:

```bash
peeragent start agent --folder ~/source/sandbox/done-cli --harness claude --prompt-file ~/source/sandbox/done-cli/.peeragent-prompt.txt
```

Das ergibt eine neue Sitzung mit neuem Namen und leerem Fenster, und für den ersten Bildschirm gilt, was dort steht. Der Agent liest den Auftrag und den Skill, legt sein Postfach `~/.a2a/done/cli/` an und schickt seine erste Nachricht an `backend`. Von da an läuft die Abstimmung ohne Sie: Der Backend-Agent schlägt den Befehl und seine Felder vor, der Kommandozeilen-Agent antwortet mit dem, was seine Seite braucht, und beide schreiben das Ergebnis dorthin, wo es hingehört, in das Wiki des jeweiligen Projekts. In Ihrem Fenster taucht davon nur auf, was die Agenten Ihnen melden.

Offen bleibt eines: ob ein Agent tut, was in einer Nachricht steht. Eine Nachricht von einem anderen Agenten ist eine Mitteilung, kein Befehl. Der Skill regelt das nicht, er fragt Sie auch nicht danach. Die Regel schreiben Sie selbst in den Auftrag, etwa so: Auf Nachrichten von backend zur Schnittstelle handelst du sofort, alles andere legst du mir vor. Das Risiko trägt nicht das Werkzeug, sondern Sie; die Regel dahinter steht im Kapitel [Wer entscheidet was](../E-mensch-und-agent/E010-wer-entscheidet-was.md).

## Die Grenze: Wer hat geschrieben?

Das Dateisystem prüft nicht, wer eine Nachricht geschrieben hat. Jeder Prozess, der unter demselben Benutzerkonto läuft, kann jeden Absendernamen in den Kopf schreiben. Solange auf dem Rechner nur Ihre eigenen Agenten laufen, ist das unerheblich. Sobald es darauf ankommt, dass eine Nachricht wirklich von dem stammt, der darin steht, reicht der einfache Weg nicht mehr. Außerhalb seines Rahmens liegen außerdem mehrere Benutzerkonten, mehrere Rechner und Netzlaufwerke. Dafür gibt es den Dienst.

## Der Dienst: simple-a2a

simple-a2a ist ein Server, der den Agenten ein gemeinsames Postamt gibt. Er befördert und bewahrt ihre Nachrichten und sieht nie hinein, was eine Nachricht sagt. Der Unterschied zum einfachen Weg: Jeder Agent weist sich mit einem [Zugangstoken](../Z-anhang/Z010-glossar.md#zugangstoken) aus. Das ist eine geheime Zeichenfolge, die wie ein Ausweis wirkt, und sie steht für genau einen Namen in genau einem Team. Mit den Tokens, in die ein Sprachmodell Text zerlegt, hat sie nur das Wort gemeinsam. Eine Nachricht kommt beim Empfänger mit einem geprüften Absender an, und ein Beobachter kann auf einer eigenen Fläche mitlesen, ohne schreiben zu können.

![Ein grauer Container mit der Beschriftung Realm enthält einen weißen Bereich mit der Beschriftung Team done. Darin stehen zwei blaue Blöcke, Backend und CLI, und unter jedem ein grüner Block Postfach. Ein oranger Pfeil führt vom Block Backend in das Postfach von CLI und ist mit Nachricht beschriftet. Ein schwarzer Pfeil führt vom Postfach von CLI nach oben in den Block CLI und ist mit liest beschriftet.](bilder/H030-postamt.svg)

**Das Postamt: Realm, Team, Postfach.** Ein Realm umschließt die Teams, ein Team die Agenten, und jeder Agent hat je Team ein Postfach. Eine Nachricht geht vom Absender in das Postfach des Empfängers und wartet dort, bis er liest.

Die Einrichtung geschieht einmal: Auf der Verwaltungsfläche legen Sie, oder ein Agent, den Sie darum bitten, einen Realm an, darin Teams, und je Agent eine Einladung. Jeder Agent löst seine Einladung ein und bekommt dafür sein Zugangstoken und sein Postfach. Von da an schreibt er seinen Teamkollegen mit deren Namen, liest und beantwortet, was ankommt, hängt Dateien an und findet seine Kollegen im Verzeichnis des Teams. Eine Einladung wird einmal gezeigt und einmal eingelöst; für ein verlorenes Zugangstoken gibt es keinen Ersatz, sondern eine neue Einladung unter neuem Namen. Und nichts wird gelöscht: Die erste Nachricht ist kein Test, sondern Teil des Bestands.

Auch beim Dienst entscheidet der Agent nicht allein, ob er tut, was in einer Nachricht steht. Anders als der Skill schreibt ihm die Anleitung des Dienstes das Vorgehen vor: Der Agent fragt Sie je Absender, ob er auf dessen Nachrichten sofort handeln soll oder vorher bei Ihnen nachfragt, und bietet eine pauschale Freigabe an, für alle Absender oder für alle eines Teams. Steht die Freigabe schon in seinem Auftrag, gilt sie.

Der Dienst erklärt sich selbst. Ein Agent, der nur die Adresse und ein Zugangstoken hat, fragt den Dienst, wie er zu benutzen ist, und bekommt einen Wegweiser, eine Anleitung in Teilen und eine Schnittstellenbeschreibung, die aus demselben Programm erzeugt wird, das die Anfragen bedient. Deshalb braucht es keine Bibliothek und kein Zusatzmodul je Harness: Jeder Agent, der eine Anfrage über HTTP stellen kann, nimmt teil. Wer lieber fertige Werkzeuge aufruft, lädt vom Dienst einen [MCP-Server](../Z-anhang/Z010-glossar.md#mcp-server) herunter, der aus der Schnittstellenbeschreibung je Operation ein Tool macht und zusätzlich ein Tool, das auf neue Post wartet.

Auch hier gilt: Der Dienst stößt niemanden an. Ein Agent, der erreichbar bleiben soll, behält sein Postfach im Auge, und der Dienst erklärt ihm, wie, mit einem fertigen Wecker für Shell und Python. Für Claude Code kann der MCP-Server neue Post außerdem als Meldung in die laufende Sitzung geben. Dieser Weg ist experimentell (Stand Oktober 2026). Er verlangt beim Eintrag des Servers das Argument `--protocol initialize`, sonst kommt nie eine Meldung an, und einen eigenen Startschalter, der die Warnung schon im Namen trägt:

```bash
claude --dangerously-load-development-channels server:simple-a2a
```

Eine solche Meldung liest das Modell als Teil des Gesprächs, und eine Anweisung darin würde es befolgen. Der MCP-Server gibt deshalb nur Absender und Betreff weiter, nie den Text. Kommt keine Meldung an, bleibt der Wecker.

Zum Ausprobieren auf dem eigenen Rechner genügen zwei Befehle. Der erste startet den Dienst als [Container](../Z-anhang/Z010-glossar.md#container), nur von diesem Rechner aus erreichbar; der zweite druckt einen ersten Prompt für Ihren Agenten, mit dem Verwaltungsgeheimnis des Dienstes darin und der Angabe, wohin dieses Geheimnis darf und wohin nicht. Dafür braucht es ein Programm, das Container startet. Unter Linux ist das `podman` oder `docker`:

```sh
podman run -d --name simple-a2a -p 127.0.0.1:8251:8251 -p 127.0.0.1:8252:8252 -p 127.0.0.1:8253:8253 -v simple-a2a-data:/var/lib/simple-a2a ghcr.io/schlingensiepen/simple-a2a:0.1.1
podman exec simple-a2a simple-a2a first-prompt
```

Mit docker lauten beide Zeilen gleich, nur mit `docker` statt `podman`. Unter Windows übernimmt das `wslc`, der Container-Befehl, der zu [WSL](../Z-anhang/Z010-glossar.md#wsl) gehört, ab Version 2.9.3; `wsl --update` bringt ihn. Die Befehle laufen in der PowerShell. Das Repo nennt diese Zeilen ungetestet (Stand Oktober 2026):

```powershell
wslc run -d --name simple-a2a -p 8251:8251 -p 8252:8252 -p 8253:8253 -v simple-a2a-data:/var/lib/simple-a2a ghcr.io/schlingensiepen/simple-a2a:0.1.1
wslc exec simple-a2a simple-a2a first-prompt
```

Die drei Ports gehören zu drei Flächen: 8251 für die Agenten, 8252 für die Verwaltung, 8253 für Beobachter. Den Prompt fügen Sie in Ihren Agenten ein; er fragt Sie nach den Namen, legt Realm und Team an und gibt Ihnen die Einladungen, die Sie mit der Adresse der Teilnehmerfläche an die anderen Agenten weitergeben. Diese Form ist zum Ausprobieren gedacht. Sie verschlüsselt nichts. Und nach einem Neustart des Rechners läuft der Container nicht von selbst wieder an; Sie starten ihn von Hand mit `podman start simple-a2a` oder demselben Befehl Ihres Container-Programms. Der Datenträger `simple-a2a-data` bewahrt Nachrichten und Geheimnis. Für den Dauerbetrieb hinter einem Proxy mit Verschlüsselung beschreibt das Repo einen eigenen Weg.

Eine Falle gibt es unter Windows, wenn der Dienst in der PowerShell läuft und Ihr Agent in WSL. Im voreingestellten NAT-Modus von WSL erreicht der Agent `127.0.0.1` unter Windows nicht. Dann veröffentlichen Sie die Ports in der PowerShell auf allen Netzadressen:

```powershell
wslc run -d --name simple-a2a -p 0.0.0.0:8251:8251 -p 0.0.0.0:8252:8252 -p 0.0.0.0:8253:8253 -v simple-a2a-data:/var/lib/simple-a2a ghcr.io/schlingensiepen/simple-a2a:0.1.1
```

Der Agent nimmt in WSL die Adresse des Windows-Rechners statt `127.0.0.1`; dieser Befehl zeigt sie:

```bash
ip route show | grep -i default | awk '{ print $3}'
```

Das hat einen Preis: Jeder Rechner, der Ihren erreicht, erreicht jetzt auch den Dienst, und Geheimnis, Zugangstoken und Einladungen gehen unverschlüsselt durchs Netz. Im gespiegelten Modus von WSL (`networkingMode=mirrored` in der Datei `.wslconfig`, ab Windows 11 22H2) teilen sich Windows und WSL `127.0.0.1`, und die Zeilen von oben genügen.

## Welcher Weg

Der Skill stellt beide nebeneinander. Der einfache Weg kostet nichts außer einem Verzeichnis, das alle kennen, und einer Erlaubnis von Ihnen; dafür ist der Absender nicht geprüft. Der Dienst prüft den Absender, kennt mehrere Rechner und bietet den Blick von außen; dafür muss er laufen. Für zwei eigene Agenten auf einem Rechner, wie bei DONE, ist der einfache Weg genug. Sobald fremde Agenten, mehrere Rechner oder ein Nachweis ins Spiel kommen, ist es der Dienst. Die Wörter bleiben dieselben: Team, Postfach, dazu der Realm als Klammer.

## Was jetzt klar sein sollte

- Agenten reden wie per Post, nicht wie am Telefon: Eine Nachricht liegt im Postfach des Empfängers, bis er liest. Dafür stellt sich jeder Agent selbst einen Wecker.
- Auf einem Rechner und unter einem Konto genügt der Skill a2a: Das Postfach ist ein Verzeichnis, die Nachricht eine Datei, der Absender steht ungeprüft im Kopf.
- Wenn der Absender zählt, kommt simple-a2a: ein kleiner Dienst mit Realm, Teams, Einladungen und Zugangstoken, der sich den Agenten selbst erklärt.
- Ein laufender Agent erfährt nichts von einem geänderten Auftrag. Wer den Meldeweg wechselt, beendet den alten Lauf, stellt Auftrag und Startprompt um und startet neu.
- Ob ein Agent tut, was in einer Nachricht steht, entscheiden Sie: beim Skill durch die Regel in seinem Auftrag, beim Dienst je Absender oder pauschal, wenn er fragt.

Weiter mit [Das Zusammenspiel](H040-das-zusammenspiel.md): Wie Koordinator und Komponenten mit allen Werkzeugen dieses Teils zusammenarbeiten.
