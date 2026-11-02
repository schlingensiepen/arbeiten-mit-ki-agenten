# Die erste Sitzung

> **Stand der Quellen:** [peeragent](https://github.com/schlingensiepen/peeragent) `v0.2.0`, `docs/harnesses.md`; weitere Angaben zu Werkzeugen gelten mit Stand Oktober 2026.

> **Eine lokale Software führt aus, was ihr jemand aus dem Internet einflüstert. Da erkennt man, dass das nicht ohne Gefahr sein kann.**

Der Agent läuft, jetzt soll er arbeiten. Dieses Kapitel führt durch die erste [Sitzung](../Z-anhang/Z010-glossar.md#sitzung), also eine zusammenhängende Arbeit mit einem Agenten von seinem Start bis zum Ende, mit einem eigenen Kontext. Die Reihenfolge ist immer dieselbe: erst der Ordner, dann der Agent, dann eine Frage, die der Agent Ihnen stellt und die Sie verstehen sollten, bevor Sie sie beantworten. Zum Schluss geht es darum, wie viel der Agent fragen soll, bevor er etwas tut.

## Erst der Ordner

Ein Agent arbeitet von dem Ordner aus, in dem Sie ihn starten. Dort liest er Dateien, dort ändert er sie, dort führt er Befehle aus. Der Ordner ist dabei sein Startpunkt, keine Grenze: Ein Befehl, den der Agent ausführt, läuft mit Ihren Rechten und kann auch Dateien außerhalb des Ordners erreichen (Stand Oktober 2026). Starten Sie ihn trotzdem nie irgendwo, sondern immer in einem Projektordner, denn dort findet er, was zum Projekt gehört. Und legen Sie den Ordner an, bevor Sie den Agenten starten, denn ein Projekt besteht aus mehreren Dateien, und ein Ordner ist ein Projekt. VS Code denkt genauso: Es öffnet keinen Dateistapel, sondern einen Ordner.

Das Beispiel für die nächsten Kapitel ist eine Lagerverwaltung. Legen Sie dafür im Terminal einen Ordner an und wechseln Sie hinein:

```bash
mkdir -p ~/source/sandbox/lager
cd ~/source/sandbox/lager
```

In VS Code öffnen Sie denselben Ordner über „File → Open Folder“. Ein Hinweis dazu: Beim Öffnen eines Ordners lädt VS Code sein Fenster neu, ein offenes Terminal ist danach weg. Öffnen Sie also erst den Ordner, dann das Terminal. Was das für einen laufenden Agenten bedeutet, ist das Thema des nächsten Kapitels.

## Dann der Agent

Im Terminal, im Projektordner, starten Sie den Agenten mit seinem Befehl, in Claude Code:

```bash
claude
```

Bei anderen Agenten heißt der Befehl anders, etwa `codex`, `copilot` oder `agy`. Beim allerersten Start fragt das Werkzeug nach der Anmeldung, wie im Kapitel [Einen Agenten bekommen](A030-einen-agenten-bekommen.md) beschrieben. Danach kommt eine Frage, die bei allen Agenten ungefähr gleich lautet.

## Die Vertrauensabfrage und ihre zwei Richtungen

Die [Vertrauensabfrage](../Z-anhang/Z010-glossar.md#vertrauensabfrage) ist die Frage des Agenten beim ersten Start in einem Ordner, ob er diesem Ordner trauen soll. Die Frage klingt nach Jargon. Sie hat aber einen Grund: Bei einem Agenten droht Gefahr aus zwei Richtungen. Die Abfrage deckt nur eine davon ab.

**Richtung 1: Was der Agent mit Befehlen vom Modell tut.** Erinnern Sie sich an den Aufbau aus dem ersten Kapitel. Das Modell schreibt Text, und in diesem Text stehen Tool-Aufrufe. Der Harness führt sie aus, ohne eigenes Urteil. Das Modell läuft beim Anbieter und schreibt, was ihm nach seinem Kontext am wahrscheinlichsten erscheint. Steht im Kontext etwas Falsches, etwa aus einer Webseite, die der Agent gerade gelesen hat, dann kann der nächste Tool-Aufruf auch „lösch diesen Ordner“ heißen. Eine Software auf Ihrem Rechner führt aus, was ihr ein Text eingibt, der von außen kommt. Davor schützt die Vertrauensabfrage nicht. Dagegen hilft, dass der Agent fragt, bevor er Dateien ändert oder Befehle ausführt. Wie oft er das tut, regelt die Berechtigungsstufe, die am Ende dieses Kapitels folgt.

**Richtung 2: Was im Ordner liegt.** Der Agent liest beim Start Dateien aus dem Ordner, allen voran die Instruktionsdatei aus dem Kapitel [Kontext](A020-kontext.md). Was dort steht, landet im Kontext und lenkt das Modell. Ein fremder Ordner kann also Anweisungen mitbringen, die Sie nicht geschrieben haben, dazu Skripte, die der Agent ausführen könnte. Gegen diese Richtung ist die Vertrauensabfrage gemacht. Vertrauen Sie dem Ordner, sagen Sie dem Agenten: Hier liegt nichts, was mich angreift.

In Claude Code ist die Ablehnung vorgewählt (Stand Oktober 2026), andere Harnesses wählen anders. Für Ihren eigenen, gerade angelegten Ordner antworten Sie mit Ja. Für einen Ordner, den Sie aus dem Netz geladen haben und noch nicht kennen, sehen Sie sich erst an, was darin liegt. VS Code stellt beim Öffnen eines Ordners dieselbe Frage, aus demselben Grund.

## Die erste eigene Datei

Geben Sie dem Agenten jetzt einen kleinen Auftrag, der eine Datei hinterlässt. Dieses Skript siezt Sie, Aufträge an den Agenten stehen aber in der Du-Form. Das ist nur kürzer, der Agent versteht beides:

```text
Lege eine Datei anforderungen.md an. Schreib hinein, was eine einfache Lagerverwaltung können muss, als Liste.
```

Der Agent fragt, ob er die Datei anlegen darf. Sie erlauben es, und die Datei erscheint links im Explorer von VS Code. Öffnen Sie sie. Sie sehen eine Textdatei: eine Zeile mit `#` davor ist eine Überschrift, Zeilen mit `-` davor sind eine Liste, drei Minuszeichen allein in einer Zeile ergeben eine Trennlinie. Das ist Markdown, ein Textformat mit wenigen Auszeichnungen, das Menschen lesen können und Modelle besonders gut. Über die Befehlspalette (F1) und „Markdown: Open Preview to the Side“ sehen Sie Quelltext und Vorschau nebeneinander; eine Änderung im Quelltext erscheint sofort rechts.

Das Wichtige daran: Das ist Ihre Datei. Sie dürfen hineinschreiben. Fehlt in der Liste etwas, etwa dass das Programm zu jedem Artikel seinen Lagerort zeigen soll, dann ergänzen Sie es selbst und reden mit dem Agenten danach weiter darüber. Er liest die Datei beim nächsten Auftrag wieder ein. Wissen, das im Projektordner liegt, gehört Ihnen und nicht dem Gespräch. Das ist die Regel aus dem Kapitel Kontext, hier zum ersten Mal in der Praxis.

Die Sitzung beenden Sie mit `/exit`.

## Wie viel der Agent fragen soll

In der ersten Sitzung hat der Agent vor jedem Schritt gefragt. Das ist der Schutz gegen die erste Richtung aus dem Abschnitt über die Vertrauensabfrage: Bevor ein Tool-Aufruf etwas ändert, sehen Sie ihn. Das lässt sich einstellen. Die Einstellung, wie weit ein Agent ohne Rückfrage handeln darf, heißt [Berechtigungsstufe](../Z-anhang/Z010-glossar.md#berechtigungsstufe), und es gibt drei davon:

1. **Einzelfreigabe.** Jede Dateiänderung und jeder Befehl wird einzeln vorgelegt. Sie sehen alles, es dauert am längsten.
2. **[Accept Edits](../Z-anhang/Z010-glossar.md#accept-edits).** Der Agent darf Dateien ohne Rückfrage ändern, für Befehle fragt er weiter. Das ist ein Kompromiss für den Alltag, aber erst sicher, wenn das Projekt unter Git steht: Dann lässt sich eine geänderte Datei zurückholen. Ohne Git ist die alte Fassung weg.
3. **[Skip Permissions](../Z-anhang/Z010-glossar.md#skip-permissions).** Der Agent handelt ohne jede Rückfrage.

In Claude Code wechselt Umschalt+Tab der Reihe nach zwischen Standard, das ist die Einzelfreigabe, Accept Edits und dem [Planmodus](../Z-anhang/Z010-glossar.md#planmodus) aus dem Kapitel [Kontext](A020-kontext.md) (Stand Oktober 2026). So schalten Sie auch den Planmodus ein. Skip Permissions verlangt dagegen beim Start den Schalter `--dangerously-skip-permissions`. Der Name sagt, was der Hersteller davon hält.

Als Einsteiger bleiben Sie bei der Einzelfreigabe, bis Ihr Projekt unter Git steht. Danach ist auch Accept Edits eine Wahl. Skip Permissions kommt nur in Frage, wenn beides zugleich gilt: Der Rechner ist wegwerfbar, es liegen also keine wertvollen Zugänge und keine wertvollen Daten darauf, und Ihre Arbeit ist per Git gesichert. Beides will geprüft sein. Ein Container wie clawbook sieht wegwerfbar aus, aber in seinem Home-Verzeichnis liegen Ihre Anmeldungen bei GitHub und den Anbietern. Und was „per Git gesichert“ bedeutet, wissen Sie erst nach dem Kapitel [Git als Gedächtnis](A060-git-als-gedaechtnis.md). Die Entscheidung über Skip Permissions fällt also frühestens danach.

Warum so vorsichtig, wo die Anbieter doch selbst aufpassen? Nach dem, was man aus der Branche hört, lassen die Anbieter die Antworten eines Modells durch ein zweites Modell prüfen, bevor sie bei Ihnen ankommen. Das fängt Grobes ab. Verlassen können Sie sich darauf nicht, denn es ist nicht Ihr Modell und nicht Ihre Regel. Mehr dazu im Hintergrundkapitel [Aufpasser-Modelle](../X-hintergrund/X030-aufpasser-modelle.md).

## Was jetzt klar sein sollte

- Erst der Ordner, dann der Agent. Ein Ordner ist ein Projekt. Für den Agenten ist er der Startpunkt, keine Grenze.
- Die Gefahr kommt aus zwei Richtungen. Die Vertrauensabfrage schützt vor dem, was ein fremder Ordner dem Modell einflüstert. Die Berechtigungsstufe schützt vor dem, was das Modell dem Harness aufträgt.
- Markdown ist Text mit wenigen Zeichen. Die Datei im Projektordner gehört Ihnen, Sie dürfen hineinschreiben.
- Drei Berechtigungsstufen: Einzelfreigabe, Accept Edits, Skip Permissions. Einsteiger bleiben bei der Einzelfreigabe, bis das Projekt unter Git steht, dann kommt Accept Edits dazu. In Claude Code wechselt Umschalt+Tab die Stufe und schaltet den Planmodus ein.

Weiter mit [Sitzungen, die weiterlaufen](A050-sitzungen-die-weiterlaufen.md): warum ein Agent stirbt, wenn das Terminal zugeht, und wie er das überlebt.
