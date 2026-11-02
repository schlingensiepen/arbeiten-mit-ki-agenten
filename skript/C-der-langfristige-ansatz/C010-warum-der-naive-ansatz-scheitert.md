# Warum der naive Ansatz scheitert

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `Vorgehen.md`.

In Teil B haben Sie etwas gebaut, und am Ende ist es an einer kleinen Änderung gebrochen. Dieses Kapitel fragt, woran das liegt. Es benennt sechs Ursachen, die alle schon im Fall steckten, und trennt sie voneinander, denn jede verlangt eine andere Antwort. Teil C begründet; die Antworten geben die Teile D bis H, und das nächste Kapitel macht daraus Anforderungen an eine Arbeitsweise.

## Parallele Wahrheiten

Im Fall aus dem Kapitel [Wo der Ansatz bricht](../B-der-naive-ansatz/B040-wo-der-ansatz-bricht.md) sagte die Spezifikation vier Befehle und der Quelltext fünf. Das ist die kleinste Form eines Problems, das bei jeder Software auftritt, die länger als eine Woche lebt. Es gibt einen Hauptzweig. Dann will ein Kunde eine Sonderversion, und jemand kopiert die Dokumente. Dann soll es eine abgespeckte Variante geben, noch eine Kopie. Jede Kopie entwickelt sich weiter, und bald gibt es zu jeder Frage drei Antworten, die alle einmal richtig waren. Das Skript nennt das parallele Wahrheiten.

Die Dokumentenkette hat dagegen kein Mittel, denn sie kennt nur das eine Dokument je Schritt. Zwei Versionen heißen zwei Ketten, und ab da gilt in beiden etwas anderes, ohne dass irgendwo steht, was.

## Die Kontextgrenze

Die zweite Ursache kennen Sie aus dem Kapitel [Kontext](../A-verstehen-und-loslegen/A020-kontext.md): Das [Kontextfenster](../Z-anhang/Z010-glossar.md#kontextfenster) ist begrenzt, und jede Sitzung beginnt leer. In der Dokumentenkette gibt es nur einen Weg, zu erfahren, was gilt: alles lesen. Alle Dokumente, den Quelltext, die Tests. Das geht in der ersten Woche. Danach wächst der Ordner, und Lesen heißt, dass das Ganze in den Kontext muss. Irgendwann passt es nicht mehr, der Agent fasst zusammen, und ausgerechnet die Einzelheit, auf die es ankam, fehlt.

Die Kette verlangt also genau das, was der Agent nicht hat: ein Gedächtnis, das alles behält. Eine Arbeitsweise, die trägt, darf nicht voraussetzen, dass jemand alles liest.

## Die starre Reihenfolge

Die Kette geht von vorn nach hinten. Das ist richtig für den ersten Durchlauf und falsch für alles danach. Beim Testen stellt sich heraus, dass eine Anforderung fehlt. Beim Bauen zeigt sich, dass eine Festlegung im Datenmodell nicht aufgeht. An Funktionen für Version 2 wird gearbeitet, während Version 1 noch nicht fertig ist. Jedes Mal müsste man vorn anfangen und alles dahinter neu schreiben, und das tut niemand, also veralten die vorderen Dokumente.

Die Vorlage, die das Skript ab Teil D benutzt, zieht daraus eine klare Folgerung. Sie sagt: Die Schritte sind ein Angebot, kein Zwang, und der Anwender darf in beliebiger Reihenfolge an ihnen arbeiten. Fehlt eine Grundlage, warnt der Agent und blockiert nicht. Was dann noch geordnet wird, und warum das reicht, ist das Thema von Teil F.

## Alles jedes Mal neu erklären

Die vierte Ursache ist unscheinbar und frisst die meiste Zeit. Jede neue Sitzung weiß nicht, wer Sie sind, wie Sie arbeiten wollen, welche Regeln gelten, was schon entschieden ist. Also erklären Sie es. Jedes Mal. Nach ein paar Wochen ist der erste Prompt einer Sitzung länger als die eigentliche Aufgabe.

Das Skript hat dafür einen Beleg, und der führt zugleich das zweite Beispiel ein. Neben der Lagerverwaltung begleitet Sie ab Teil D eine Aufgabenverwaltung mit dem Namen DONE. Ihr [Startprompt](../Z-anhang/Z010-glossar.md#startprompt) aus der Zeit, als es noch keine Arbeitsweise dafür gab, steht in voller Länge im Beispiel [DONE ohne Regelwerk](../Y-beispiele/Y030-done-ohne-regelwerk.md). Lesen Sie ihn nicht, um ihn zu benutzen, dafür ist er nicht gedacht. Lesen Sie ihn, um zu sehen, wie viel man einem Agenten sagen muss, damit er so arbeitet, wie man es will, und stellen Sie sich vor, das jede Sitzung neu zu tun.

## Niemand prüft unabhängig

Im Kapitel [Bauen und prüfen](../B-der-naive-ansatz/B030-bauen-und-pruefen.md) war es schon zu sehen: Der Agent, der gebaut hat, schreibt auch die Tests, in demselben Kontext, mit denselben Missverständnissen. Grün heißt, dass das Programm zu seinem eigenen Verständnis passt. Sie prüfen dagegen, aber Sie können nicht alles lesen, und Sie prüfen gegen Dokumente, die derselbe Agent geschrieben hat.

Die Vorlage setzt dagegen Prüfungen vor jede Freigabe, durch einen oder mehrere Prüfer, die nicht mitgeschrieben haben und mit eigenem Kontext lesen. Wie das geht, zeigt das Kapitel [Prüfen](../G-der-gesamtprozess/G020-pruefen.md). Die Ursache lässt sich jetzt schon benennen: Im naiven Ansatz gibt es keinen Platz für einen zweiten Blick.

## Arbeitsmaterial und Ergebnis liegen durcheinander

Sehen Sie sich den Projektordner am Ende von Teil B an. Darin liegen die Anforderungen, Notizen aus dem Gespräch, ein Datenmodell, eine Spezifikation, deren Stand unklar ist, der Quelltext, die Tests, vielleicht eine Kopie der Anforderungen für Version 2. Wer das Programm haben will, bekommt alles davon mit. Wer weiterarbeiten will, muss erst herausfinden, was davon aktuell ist und was Arbeitsmaterial war.

Beides gehört getrennt: das, womit man arbeitet, und das, was man weitergibt. Wie die Vorlage das trennt und wie das Ergebnis aus dem Arbeitsmaterial entsteht, zeigt das Kapitel [Werkstatt, Produkt, Schleuse](../G-der-gesamtprozess/G030-werkstatt-produkt-schleuse.md).

## Was jetzt klar sein sollte

- Der naive Ansatz scheitert nicht an einem Fehler, sondern an sechs Ursachen, die beim ersten Durchlauf unsichtbar sind.
- Parallele Wahrheiten: Kopien von Dokumenten entwickeln sich auseinander, und nirgends steht, was gilt.
- Die Kontextgrenze: Die Kette setzt voraus, dass jemand alles liest. Der Agent kann das nicht.
- Die starre Reihenfolge: Jede späte Erkenntnis müsste vorn eingearbeitet werden, also veralten die vorderen Dokumente.
- Alles neu erklären: Jede Sitzung beginnt bei null. Das Beispiel DONE ohne Regelwerk zeigt, was das kostet.
- Niemand prüft unabhängig, und Arbeitsmaterial und Ergebnis liegen im selben Ordner.

Weiter mit [Anforderungen an eine Arbeitsweise](C020-anforderungen-an-eine-arbeitsweise.md): Aus den sechs Ursachen werden sieben Forderungen.
