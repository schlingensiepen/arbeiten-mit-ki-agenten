# Lagerverwaltung

> **Stand der Quellen:** keine gebundene Quelle. Der Prompt ist für dieses Skript geschrieben.

Dies ist der [Startprompt](../Z-anhang/Z010-glossar.md#startprompt) für das erste Beispiel des Skripts, die Lagerverwaltung. Mit ihm beginnt in Teil B der naive Ansatz: ein [Agent](../Z-anhang/Z010-glossar.md#agent), ein leerer Ordner und dieser Text, sonst nichts. Kein Regelwerk, keine Vorlage, keine Vorbereitung. Der Prompt ist zum Nachmachen gedacht. Kopieren Sie ihn, geben Sie ihn Ihrem Agenten als erste Nachricht, und arbeiten Sie mit.

## Was der Prompt erreichen soll

Wer einem Agenten „schreib mir eine Lagerverwaltung“ sagt, bekommt Code. Sofort, und ziemlich viel davon. Das ist der Code-Impuls, und er ist das Problem: Der Agent baut dann etwas, das niemand so bestellt hat, weil niemand vorher gesagt hat, was gebraucht wird. Der Prompt steuert dagegen. Er sagt, worum es geht, und verbietet im selben Atemzug den Code. Zuerst werden die Anforderungen entwickelt, im Gespräch: Der Agent fragt, Sie entscheiden.

Das Zweite, was der Prompt tut: Er hält das Vorhaben klein. Ein Benutzer, ein Lagerort je Artikel, Bedienung im Terminal, eine Liste statt eines Bestellvorschlags. Alles, was man weglassen kann, wird weggelassen. Was der Prompt an Fachlichem vorgibt, ist bewusst wenig. Den Rest soll der Agent erfragen.

## Der Prompt

```text
Ich möchte ein Lagerverwaltungsprogramm schreiben. Schreib noch keinen Code. Wir entwickeln erst die Anforderungen.

Das Programm bleibt klein:
- Ein Benutzer an einem Rechner. Kein Mehrbenutzerbetrieb, kein Netz.
- Ein einfaches Lager: Jeder Artikel hat einen Bestand und genau einen Lagerort. Keine Chargen.
- Bedienung im Terminal, keine grafische Oberfläche.
- Statt eines Bestellvorschlags reicht eine Liste der Artikel, deren Bestand unter einer Mindestmenge liegt. Bestellen entscheide ich selbst.

Was ich schon weiß:
- Es gibt Artikel, Lagerorte und Bewegungen. Eine Bewegung ist ein Zugang oder ein Abgang mit Menge und Datum.
- Der Bestand eines Artikels ergibt sich aus seinen Bewegungen.
- Artikel werden nicht gelöscht, sondern inaktiv gesetzt, damit alte Bewegungen weiter auf sie zeigen.

So arbeiten wir:
- Du fragst, ich entscheide. Stell mir deine Fragen einzeln, mit einem Satz dazu, warum die Antwort wichtig ist, und mit deinem Vorschlag.
- Wenn du eine Lücke in meinen Angaben siehst, sprich sie an, statt sie mit einer Annahme zu füllen.
- Schreib die Anforderungen, auf die wir uns einigen, in eine Datei anforderungen.md: nummeriert, je Anforderung ein Satz.
- Datenmodell, Abläufe und Code kommen erst, wenn ich die Anforderungen bestätigt habe.
```

## Wie Sie ihn benutzen

Legen Sie einen leeren Ordner an und starten Sie darin Ihren Agenten. Wie das geht und was er Sie beim Start fragt, steht in [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md). Dann fügen Sie den Prompt als erste Nachricht ein.

Der Agent wird keinen Code schreiben, sondern fragen. Antworten Sie, als wäre es Ihr Lager. Es gibt keine falschen Antworten, nur unbeantwortete Fragen. Wenn der Agent etwas vorschlägt, das Ihnen nicht passt, sagen Sie es. Wenn er etwas annimmt, statt zu fragen, weisen Sie ihn darauf hin. Wie dieses Gespräch läuft und worauf Sie dabei achten, zeigt [Anforderungen im Gespräch](../B-der-naive-ansatz/B010-anforderungen-im-gespraech.md).

Statt des Satzes „Schreib noch keinen Code“ können Sie auch den [Planmodus](../Z-anhang/Z010-glossar.md#planmodus) Ihres Agenten einschalten. Er bewirkt dasselbe: Der Agent legt erst vor, statt zu handeln. Was das technisch ist, steht in [Kontext](../A-verstehen-und-loslegen/A020-kontext.md).

## Was danach kommt

Der Prompt endet bei den Anforderungen, mit Absicht. Die letzte Zeile nennt schon, wie es weitergeht: Datenmodell, Abläufe, Code. Im naiven Ansatz folgt je Schritt ein Dokument, jedes mit einem neuen Prompt in derselben Sitzung. Diese Kette und ihre Glieder zeigt [Die Dokumentenkette](../B-der-naive-ansatz/B020-die-dokumentenkette.md), das Bauen und Prüfen zeigt [Bauen und prüfen](../B-der-naive-ansatz/B030-bauen-und-pruefen.md). Wo die Kette zur Last wird, steht in [Wo der Ansatz bricht](../B-der-naive-ansatz/B040-wo-der-ansatz-bricht.md).

Behalten Sie den Prompt im Kopf. Er enthält unter „So arbeiten wir“ vier Regeln, die Sie jedem Agenten in jedem Projekt wieder sagen müssten. Das zweite Beispiel des Skripts, die Aufgabenverwaltung DONE, zeigt in [DONE mit Referenzprozess](Y020-done-mit-referenzprozess.md), wie ein Startprompt aussieht, wenn ein Regelwerk diese Regeln übernimmt, und in [DONE ohne Regelwerk](Y030-done-ohne-regelwerk.md), was es kostet, wenn man alles selbst sagt.
