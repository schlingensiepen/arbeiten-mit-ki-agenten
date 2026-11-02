# Kontext

> **Stand der Quellen:** keine gebundene Quelle; Angaben zu Werkzeugen gelten mit Stand Oktober 2026.

> **Durchlesen heißt immer: Das Ganze muss in den Kontext. Und der Kontext ist unser heiliges Gut.**

Im Kapitel [Was ein Agent ist](A010-was-ein-agent-ist.md) kam der Kontext nur am Rand vor: Alles, was dem Modell bei einer Antwort vorliegt, und der Platz dafür ist begrenzt. Dieses Kapitel nimmt den Satz ernst. Es zeigt, was im Kontext liegt, warum er bei jeder Runde neu aufgebaut wird, was passiert, wenn er voll ist, und wie Sie ihn beobachten. Am Ende steht eine Regel, die den Rest dieses Skripts trägt: Was Sie mit dem Agenten erarbeiten, gehört in Dateien, nicht in das Gespräch.

## Das Modell erinnert sich nicht

> **Das Modell erinnert sich nicht. Bei jeder Antwort wird ihm das ganze Gespräch noch einmal vorgelegt.**

Ein Sprachmodell hat keinen Zustand zwischen zwei Aufrufen. Es bekommt Text und schreibt ihn weiter, dann ist der Aufruf vorbei. Dass sich ein Gespräch trotzdem über viele Fragen trägt, besorgt der Harness: Bei jeder neuen Frage schickt er das gesamte bisherige Gespräch noch einmal mit, die eigene Frage hinten dran. Darum versteht das Modell nach einer Frage zum VW Käfer auch die Anschlussfrage „Und was war mit den blauen?“: Die erste Frage steht im Prompt.

Die Folge ist unauffällig, aber wichtig. Der Prompt wächst mit jeder Runde. Jede Frage, jede Antwort und jedes Tool-Ergebnis kommt dazu und bleibt dabei, denn alles muss bei der nächsten Runde wieder vorgelegt werden.

## Was im Fenster liegt

Der Platz, der dem Modell für einen Aufruf zur Verfügung steht, heißt [Kontextfenster](../Z-anhang/Z010-glossar.md#kontextfenster). Es hat eine feste Größe, weil das Modell in endlicher Zeit rechnen muss. Gemessen wird es nicht in Wörtern, sondern in [Tokens](../Z-anhang/Z010-glossar.md#token): Das sind die Stücke, in die ein Modell Text zerlegt. Ein kurzes Wort ist oft ein Token, ein langes deutsches Wort wie „Feuerwehrfahrzeug“ wird in mehrere zerlegt. Als Faustregel reicht: ein Token ist etwa ein Wort oder ein Wortteil. In Tokens werden auch die Kosten abgerechnet, dazu unten mehr.

Das Fenster ist nicht leer, wenn Sie Ihre erste Frage stellen. Beim Start liegen schon darin:

- der [Systemprompt](../Z-anhang/Z010-glossar.md#systemprompt), die Grundausrichtung, die der Anbieter ganz vorn setzt;
- die Beschreibungen aller Tools, denn das Modell kann nur aufrufen, was ihm vorher vorgestellt wurde;
- die Beschreibungen der Skills, zu denen gleich mehr kommt;
- die [Instruktionsdatei](../Z-anhang/Z010-glossar.md#instruktionsdatei), eine Datei im Projektordner, die der Agent beim Start von selbst lädt, in Claude Code etwa `CLAUDE.md`. Jedes Wort darin kostet Platz, bei jeder Runde. Was in diese Datei gehört und was nicht, ist Thema des Kapitels [Regelwerk und Sessionstart](../D-wissen-im-wiki/D020-regelwerk-und-sessionstart.md).

Erst danach kommt das Gespräch: Ihre Aufträge, die Antworten des Modells und die Ergebnisse der Tools. Besonders die Tool-Ergebnisse fallen ins Gewicht. Liest der Agent eine Datei, landet ihr Inhalt vollständig im Kontext, denn anders kann das Modell ihn nicht sehen. Durchlesen heißt für einen Agenten immer: Das Ganze kommt ins Fenster. Eine lange Dokumentation einzulesen, „um sie zu kennen“, ist deshalb keine harmlose Bitte.

## Skills und Planmodus sind auch nur Prompt

Zwei Dinge, die in den Werkzeugen wie besondere Fähigkeiten aussehen, lassen sich mit dem Kontext erklären.

Ein [Skill](../Z-anhang/Z010-glossar.md#skill) ist eine Anleitung für eine bestimmte Art von Aufgabe, die als Datei bereitliegt. Im Kontext steht beim Start nur ein kurzer Hinweis der Art: Wenn du das tun willst, lies diese Datei. Die Anleitung selbst lädt der Agent erst, wenn er sie braucht. Das spart Kontext. Wer in einer Sitzung keine E-Mail verschickt, liest den Skill dafür nicht. Würde man dem Agenten alles vorab beibringen, wäre das Fenster voll, bevor die Arbeit beginnt.

Der [Planmodus](../Z-anhang/Z010-glossar.md#planmodus) ist eine Betriebsart, in der der Agent erst einen Plan vorlegt, statt zu handeln. Technisch ist auch das ein weiteres Stück Prompt: Der Harness sagt dem Modell, dass es jetzt planen und nicht ausführen soll. Den fertigen Plan legt er in einer Datei ab, und das Modell hakt die erledigten Schritte ab. Dass der Plan in einer Datei liegt und nicht nur im Gespräch, ist kein Zufall. Der Grund folgt im nächsten Abschnitt.

## Wenn das Fenster voll ist

Irgendwann passt nichts mehr hinein. Schon vorher werden die Antworten oft schlechter, weil das Modell in sehr viel Text das Wesentliche schwerer findet. Beim vollen Fenster bleiben zwei Möglichkeiten, und beide kosten etwas:

1. **Abschneiden.** Der Harness lässt das Älteste weg. Dann fehlt es.
2. **Zusammenfassen.** Das Modell selbst fasst das bisherige Gespräch zusammen, und die Zusammenfassung ersetzt den Verlauf. Das Verfahren heißt [Compact](../Z-anhang/Z010-glossar.md#compact), es läuft bei vielen Harnesses von selbst, wenn das Fenster voll wird, oder auf Befehl. Damit das Modell dafür Platz hat, hält der Harness einen Teil des Fensters frei.

Beim Zusammenfassen entscheidet das Modell, was wichtig war. Ein Beispiel: Sie haben mit dem Agenten zwei Ideen besprochen, ein Blinklicht und einen Personenzähler. Ist eine davon verworfen, fällt die Zusammenfassung leicht. Sind beide wichtig, gehen trotzdem Einzelheiten verloren, denn genau das ist der Zweck einer Zusammenfassung.

> **Nach dem Komprimieren ist ein Agent dümmer. Es fehlt ja was.**

Das ist kein Fehler eines bestimmten Werkzeugs, sondern liegt im Prinzip. Deshalb achtet man bei der Arbeit mit Agenten auf das Fenster, so wie man bei einem Rechner auf den Arbeitsspeicher achtet.

## Kontext als Haushalt

Weil der Kontext begrenzt ist und jede Runde ihn ganz neu vorlegt, lohnt es sich, ihn wie einen Haushalt zu führen: wissen, was drin ist, wissen, was es kostet, und nachsehen, bevor es knapp wird.

**Kosten.** Bezahlt werden Tokens, die hineingehen, und Tokens, die herauskommen. Entweder direkt je Token oder aus einem Kontingent, das zu einem Abo gehört. Ein volles Fenster, das bei jeder Runde neu vorgelegt wird, kostet darum bei jeder Runde. Eine Datei, die der Agent nicht braucht, aber gelesen hat, kostet bis zum Ende der Sitzung mit.

**Beobachten.** Jeder Harness hat einen Befehl, der die Belegung des Fensters anzeigt. In Claude Code heißt er `/context`. Die Anzeige teilt das Fenster in Posten auf: Systemprompt, Tool-Beschreibungen, Skills, die Nachrichten des Gesprächs, dazu den Platz, der für das Zusammenfassen frei bleibt. Sehen Sie sich das in Ihren ersten Sitzungen regelmäßig an. Sie bekommen so ein Gefühl dafür, wie schnell das Fenster wächst und was es füllt, bevor es zur Neige geht. Die Zahlen selbst, wie groß ein Fenster ist und was ein Token kostet, ändern sich schnell und stehen deshalb nicht in diesem Skript.

## Unterhaltung vergeht, Dateien bleiben

> **Das Kontextfenster ist begrenzt. Was Sie ausarbeiten, gehört auf die Platte.**

Jetzt lässt sich die Regel begründen, mit der das Kapitel begonnen hat. Das Gespräch mit dem Agenten ist wie der Arbeitsspeicher eines Rechners: schnell, aber begrenzt, und mit dem Ende der Sitzung weg. Wird das Fenster zusammengefasst, fehlt ein Teil. Stürzt der Agent ab oder wollen Sie morgen weitermachen, ist das Gespräch nicht mehr da. Eine Datei im Projektordner dagegen bleibt, wie eine Datei auf der Platte. Der Agent kann sie in der nächsten Sitzung wieder lesen, und zwar nur den Teil, den er gerade braucht.

![Links ein Container Kontextfenster mit drei Blöcken untereinander: Systemprompt mit Tools, Skills und Instruktionsdatei, darunter Gespräch mit Fragen, Antworten und Tool-Ergebnissen, darunter gestrichelt frühere Runden, zusammengefasst. Rechts ein Container Projektordner mit zwei Dateien, anforderungen.md und plan.md. Ein oranger Pfeil führt vom Gespräch zur Datei, beschriftet Datei schreiben, ein schwarzer Pfeil zurück, beschriftet Datei lesen.](bilder/A020-arbeitsspeicher-und-platte.svg)

**Unterhaltung vergeht, Dateien bleiben.** Das Kontextfenster wird je Runde neu gefüllt und beim Zusammenfassen gekürzt. Was der Agent in eine Datei schreibt, bleibt im Projektordner und kommt bei Bedarf wieder in den Kontext.

Daraus folgt eine Arbeitsweise. Haben Sie mit dem Agenten etwas erarbeitet, etwa die Anforderungen an eine Lagerverwaltung, dann lassen Sie es ihn in eine Datei schreiben. Schlägt er das nicht selbst vor, verlangen Sie es: „Schreib die Anforderungen in die Datei `anforderungen.md`.“ Das Schreiben ist ein gewöhnlicher Tool-Aufruf, Sie sehen ihn im Verlauf. Danach ist der Zwischenstand gesichert, für morgen und für den Fall, dass der Agent abstürzt. Wie aus solchen Dateien ein Gedächtnis wird, in dem der Agent nur liest, was er braucht, zeigt der Teil [Wissen im Wiki](../D-wissen-im-wiki/D010-das-wiki.md).

## Was jetzt klar sein sollte

- Das Modell erinnert sich nicht. Der Harness legt ihm bei jeder Runde das ganze Gespräch neu vor, deshalb wächst der Prompt.
- Das Kontextfenster ist begrenzt und wird in Tokens gemessen. Beim Start liegen schon Systemprompt, Tool-Beschreibungen, Skills und Instruktionsdatei darin; jede gelesene Datei kommt vollständig dazu.
- Skills und Planmodus sind weitere Stücke Prompt. Skills sparen Kontext, weil sie erst bei Bedarf geladen werden.
- Ist das Fenster voll, wird abgeschnitten oder zusammengefasst. In beiden Fällen fehlt danach etwas.
- Beobachten Sie das Fenster mit dem Befehl des Harness. Was Sie ausarbeiten, gehört in eine Datei.

Weiter mit [Einen Agenten bekommen](A030-einen-agenten-bekommen.md): die Wege zu einem eigenen Agenten und ein fertig eingerichteter Arbeitsrechner.
