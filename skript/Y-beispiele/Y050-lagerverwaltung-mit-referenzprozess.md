# Lagerverwaltung mit Referenzprozess

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `README.md`, `INIT.md`.

Dies ist derselbe Stoff wie in [Lagerverwaltung](Y010-lagerverwaltung.md), aber als [Startprompt](../Z-anhang/Z010-glossar.md#startprompt) für den [Referenzprozess](../Z-anhang/Z010-glossar.md#referenzprozess). Wer Teil D gelesen hat, kann die Lagerverwaltung damit noch einmal aufsetzen und sieht am eigenen Beispiel, was sich ändert.

## Der Prompt

```text
Richte dieses Verzeichnis als neues Projekt nach der Anleitung unter https://github.com/schlingensiepen/referenzprozess-softwareentwicklung ein.

git init, das Einbinden der Vorlage und das Kopieren der Projektdateien darfst du ausführen, jeweils auf dem Weg, den du empfiehlst.

Das Projekt: ein Lagerverwaltungsprogramm. Es bleibt klein:
- Ein Benutzer an einem Rechner. Kein Mehrbenutzerbetrieb, kein Netz.
- Ein einfaches Lager: Jeder Artikel hat einen Bestand und genau einen Lagerort. Keine Chargen.
- Bedienung im Terminal, keine grafische Oberfläche.
- Statt eines Bestellvorschlags reicht eine Liste der Artikel, deren Bestand unter einer Mindestmenge liegt. Bestellen entscheide ich selbst.

Was ich schon weiß:
- Es gibt Artikel, Lagerorte und Bewegungen. Eine Bewegung ist ein Zugang oder ein Abgang mit Menge und Datum.
- Der Bestand eines Artikels ergibt sich aus seinen Bewegungen.
- Artikel werden nicht gelöscht, sondern inaktiv gesetzt, damit alte Bewegungen weiter auf sie zeigen.

An vielen Stellen bin ich oberflächlich geblieben. Was du fachlich nicht verstehst oder nur mit Annahmen umsetzen kannst, frag mich nach dem Einrichten.
```

## Was sich gegenüber dem ersten Prompt ändert

Der Prompt hat denselben Aufbau wie [DONE mit Referenzprozess](Y040-done-mit-referenzprozess.md): Startsatz, Erlaubnis, Beschreibung. Der fachliche Teil steht fast wörtlich auch im ersten Prompt der Lagerverwaltung.

Weg ist der Abschnitt „So arbeiten wir“ und damit auch der Satz „Schreib noch keinen Code“. Dass der Agent fragt und Sie entscheiden, dass er Lücken anspricht und dass Anforderungen nummeriert festgehalten werden, regelt das Regelwerk. Sie müssen es nicht mehr sagen. Die Anforderungen landen darum auch nicht in einer Datei `anforderungen.md`, sondern als Einträge im [Wiki](../Z-anhang/Z010-glossar.md#wiki).

Ein Satz zum [Koordinator](../Z-anhang/Z010-glossar.md#koordinator) fehlt, anders als bei DONE: Die Lagerverwaltung ist ein einzelnes Programm, und die Vorauswahl der Vorlage passt.

## Wie Sie ihn benutzen

Legen Sie einen leeren Ordner an und starten Sie darin Ihren Agenten, nicht im Ordner des ersten Versuchs. Sie brauchen Internet, weil der Agent die Anleitung und die Vorlage von GitHub holt. Fügen Sie den Prompt als erste Nachricht ein. Der Ablauf und die Fragen sind dieselben wie in [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md); als Rolle bleibt es bei der Vorauswahl.

Weiter mit [DONE mit Referenzprozess](Y040-done-mit-referenzprozess.md).
