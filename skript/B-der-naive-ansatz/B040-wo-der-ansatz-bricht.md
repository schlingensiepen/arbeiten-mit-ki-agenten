# Wo der Ansatz bricht

> **Stand der Quellen:** keine gebundene Quelle. Dieses Kapitel führt einen Fall durch.

Die Lagerverwaltung läuft. Die Anforderungen stehen in einer Datei, das Datenmodell in der nächsten, die Spezifikation in der dritten, der Quelltext liegt daneben, die Tests sind grün. Bis hierher hat der naive Ansatz getragen. Dieses Kapitel zeigt an einem Fall, wo er bricht. Es erklärt noch nicht, warum; das tut Teil C. Hier geht es nur darum, den Bruch einmal gesehen zu haben.

## Eine Änderung kommt

Stellen Sie sich vor, nach einer Woche fällt auf: Jemand hat eine Auslagerung falsch gebucht, zehn Pakete statt einem. Der Bestand stimmt nicht mehr. Löschen scheidet aus, das haben Sie im ersten Kapitel festgelegt, denn das Protokoll soll vollständig bleiben. Also braucht das Programm eine neue Bewegungsart: ein Storno, das auf die falsche Bewegung verweist und ihre Wirkung aufhebt. Eine kleine Änderung, fachlich sauber, in fünf Minuten erklärt.

Jetzt gehen Sie die Kette ab:

1. **Anforderungen.** Eine neue Anforderung: Eine Bewegung kann storniert werden.
2. **Datenmodell und Abläufe.** Eine neue Bewegungsart, ein Verweis auf die stornierte Bewegung, ein neuer Ablauf Stornieren.
3. **Spezifikation.** Ein neuer Befehl. Was er prüft: Gibt es die Bewegung? Ist sie schon storniert? Wäre der Bestand danach negativ?
4. **Implementierung.** Der Quelltext für all das.
5. **Test.** Prüfungen für den neuen Befehl und seine Randfälle.

Fünf Dokumente für eine Änderung, die in einem Satz passt. Das ist der Preis der Kette, und beim ersten Durchlauf fiel er nicht auf, weil jedes Dokument ohnehin neu entstand.

## Was dabei schiefgeht

Was Sie wahrscheinlich tun, ist das hier: Sie sagen dem Agenten „Bau ein Storno ein“. Er tut, was Sie sagen. Er ändert den Quelltext und, wenn Sie Glück haben, die Tests. Die Anforderungen und die Spezifikation bleiben, wie sie waren, denn niemand hat ihm gesagt, dass auch sie dran sind. Von außen ist alles gut: Das Programm kann stornieren, die Tests sind grün.

Jetzt gibt es im Projektordner zwei Wahrheiten. Die Spezifikation sagt, es gibt vier Befehle. Der Quelltext hat fünf. Solange Sie beides im Kopf haben, stört das nicht. Aber Sie haben es nicht lange im Kopf, und der Agent erst recht nicht.

Denn die nächste [Sitzung](../Z-anhang/Z010-glossar.md#sitzung) beginnt mit leerem Kontext, so war es im Kapitel [Kontext](../A-verstehen-und-loslegen/A020-kontext.md). Der Agent weiß nichts vom Storno. Soll er die nächste Änderung einbauen, liest er die Spezifikation, und die kennt kein Storno. Je nachdem, was Sie ihn fragen, baut er das Storno ein zweites Mal, baut daran vorbei oder meldet einen Widerspruch zwischen Dokument und Quelltext, den Sie dann aufklären müssen. Der Ausweg wäre, dass er jedes Mal alles liest, alle Dokumente und den ganzen Quelltext. Das kostet genau das, was knapp ist: den Kontext.

Und das war eine Änderung. Nach der dritten und fünften weiß niemand mehr, welches Dokument welchen Stand hat. Die Dokumente, die am Anfang die Stärke des Ansatzes waren, werden zur Altlast. Man hört auf, sie zu lesen, weil man ihnen nicht mehr traut, und dann kann man sie auch weglassen.

## Der zweite Fall: zwei Versionen zugleich

Nehmen Sie dazu den Fall aus dem Kapitel [Die Dokumentenkette](B020-die-dokumentenkette.md): Version 1 der Lagerverwaltung ist im Einsatz, und Version 2 soll mehrere Benutzer können. Daran arbeiten Sie jetzt mit dem Agenten. Die Anforderungen für Version 2 sind andere als für Version 1, also kopieren Sie die Datei: eine für Version 1, eine für Version 2. Dasselbe mit dem Datenmodell, der Spezifikation, dem Quelltext. Aus einer Kette werden zwei.

Dann kommt das Storno. Es gehört in Version 1, denn dort wird gearbeitet. Es gehört auch in Version 2, denn die soll alles können, was Version 1 kann. Eine Änderung, zwei Ketten, zehn Dokumente. Und bei jedem Dokument die Frage, ob die Kopie noch mit dem Original übereinstimmt oder sich schon auseinanderentwickelt hat.

## Die Kette wird zur Last

Zusammengenommen: Jede Änderung berührt jedes Dokument hinter ihr. Die Kette funktioniert nur, wenn jede Änderung durch alle Dokumente läuft. Der Agent tut, was man ihm sagt, und nicht mehr. Die nächste Sitzung weiß nicht, was gilt, und alles zu lesen kostet den Kontext. Gibt es mehrere Versionen, verdoppelt sich das alles.

Beim ersten Durchlauf trägt die Kette. Bei Änderungen trägt man die Kette.

Was nicht gebrochen ist, soll auch gesagt sein: Die Dokumente selbst sind richtig. Anforderungen vor dem Code, ein Datenmodell, eine Spezifikation, Tests, das bleibt. Gebrochen ist die Art, wie sie zusammenhängen und wie sie gepflegt werden. Teil C nimmt den Fall auseinander und fragt, woran es wirklich liegt.

## Was jetzt klar sein sollte

- Eine fachlich kleine Änderung berührt alle Dokumente hinter ihr. Beim ersten Durchlauf fällt das nicht auf, danach jedes Mal.
- Der Agent ändert, was man ihm sagt. Was er nicht ändert, veraltet still, und dann stehen zwei Wahrheiten im Ordner.
- Die nächste Sitzung weiß nicht, welches Dokument gilt. Alles zu lesen kostet den Kontext.
- Mehrere Versionen verdoppeln die Kette und mit ihr jede Änderung.

Weiter mit [Warum der naive Ansatz scheitert](../C-der-langfristige-ansatz/C010-warum-der-naive-ansatz-scheitert.md): die Ursachen hinter dem Fall.
