# Anforderungen im Gespräch

> **Stand der Quellen:** keine gebundene Quelle. Dieses Kapitel beschreibt kein Werkzeug, sondern ein Gespräch.

> **Zu beschreiben, was das Problem ist, was der Use Case und was die Anforderungen sind: Das ist der Kern dessen, was wir lernen wollen.**

Am Ende von Teil A läuft ein [Agent](../Z-anhang/Z010-glossar.md#agent) in Ihrem Projektordner. Jetzt soll er etwas bauen. Das Beispiel für diesen Teil ist eine Lagerverwaltung: Artikel kommen herein, Artikel gehen hinaus, und jemand will wissen, was da ist. Sie müssen dafür kein Lager kennen, das Lager ist nur das Beispiel. Ein anderes handhabbares Beispiel wäre ein Restaurant mit Online-Bestellung. Wichtig ist nur, dass es kein Riesending ist.

Der naheliegende Weg wäre, dem Agenten zu sagen: „Programmier mir eine Lagerverwaltung.“ Er würde es tun, sofort. Dieses Kapitel zeigt, warum Sie das nicht tun und was Sie stattdessen tun: Sie erarbeiten mit dem Agenten im Gespräch, was das Programm können soll, bevor eine Zeile Code entsteht. Diese Beschreibung heißt Anforderungen. Der ganze Teil B geht dann den direkten Weg von den Anforderungen zum fertigen Programm. Das Skript nennt diesen Weg den naiven Ansatz, denn Teil C zeigt, wo er bricht. Erst tun, dann begründen.

## Der erste Satz entscheidet

> **Was Sie ihm als Arbeitsauftrag geben, macht er. Sagen Sie „programmieren“, bekommen Sie Quelltext, nicht Anforderungen.**

Der Agent treibt vorwärts. Steht im [Prompt](../Z-anhang/Z010-glossar.md#prompt) „schreib ein Programm“, schreibt er ein Programm. Steht dort „entwickle mit mir die Anforderungen“, stellt er Fragen. Der erste Satz legt fest, was in den nächsten zwanzig Minuten passiert. Ein Satz, der funktioniert:

```text
Ich möchte ein Lagerverwaltungsprogramm schreiben und dazu erst einmal die Anforderungen entwickeln. Schreib noch keinen Code, kläre erst mit mir, was das Programm können soll.
```

Es gibt zwei Wege, dem Agenten das Bauen vorerst zu verbieten. Der erste steht im Satz oben: Sie sagen es ihm. Der zweite ist der [Planmodus](../Z-anhang/Z010-glossar.md#planmodus) aus dem Kapitel [Kontext](../A-verstehen-und-loslegen/A020-kontext.md): Darin legt der Agent erst einen Plan vor, statt zu handeln. Beides wirkt gleich, der Planmodus ist nur ein weiteres Stück Prompt, das der Harness für Sie schreibt. Ein vollständiger Startprompt für die Lagerverwaltung zum Nachmachen steht im Beispiel [Lagerverwaltung](../Y-beispiele/Y010-lagerverwaltung.md).

Warum erst reden? Weil der Agent nicht weiß, was Sie wollen. Er weiß, wie Lagerverwaltungen üblicherweise aussehen, und baut dann eine übliche. Ob die zu Ihrem Lager passt, erfährt er nur von Ihnen.

## Der Agent fragt, Sie entscheiden

Die Rollen in diesem Gespräch sind klar verteilt. Der Agent stellt die Fachfragen, denn er kennt die üblichen Fälle und weiß, was man bei einer Lagerverwaltung alles festlegen muss. Sie beantworten, was Sie wissen, und entscheiden, was offen ist. Niemand sonst kann das, denn es ist Ihr Lager.

Einige Fragen, die in so einem Gespräch kommen:

- Wie wird ein Artikel gezählt? Nach Stück, nach Gewicht? Soll eine Waage angeschlossen werden, oder werden Packungen gebucht? Das ist eine fachliche Frage mit einer technischen Antwort, und sie entscheidet viel.
- Wie viele Artikel liegen an einem Lagerort, und an wie vielen Orten liegt ein Artikel? Tausend Pakete Taschentücher passen nicht in ein Fach. Solche Fragen nach dem „wie viele von was zu was“ klingen harmlos und bestimmen das ganze Datenmodell.
- Wird das Gewicht in Gramm als ganze Zahl geführt? Kommazahlen machen beim Eingeben Ärger. Ein kleines Beispiel dafür, dass eine Festlegung Folgen hat, die man erst später sieht.
- Welche Auswertungen braucht jemand? „Alles, was unter dem Mindestbestand liegt“ ist eine Suche, auf die man erst kommen muss, und die man besser jetzt festlegt als nach dem Bauen.

Der Agent weist dabei von selbst auf Randfälle hin, die man ohne ihn zunächst übersieht, englisch Edge Cases: Was passiert, wenn mehr ausgelagert wird, als da ist? Was, wenn ein Artikel an zwei Orten liegt? Sie können ihn auch ausdrücklich danach fragen. Technische Fragen, etwa nach der Datenbank, vertagen Sie in diesem Gespräch. Sie gehören in einen späteren Schritt.

Eine Erfahrung, die sich in solchen Gesprächen wiederholt: Alle Beteiligten erwarten bei einer Funktion dasselbe, und niemand hat es dem Agenten gesagt. Was für Sie selbstverständlich ist, ist für den Agenten eine offene Frage, und er füllt offene Fragen mit dem Üblichen.

## Die Beispielkette: so wächst das Lager

Für die Lagerverwaltung ergibt sich im Gespräch eine Kette von Festlegungen, die Sie bei fast jeder Software wiederfinden.

**Das Datenmodell.** Dinge der echten Welt bekommen eine Repräsentation mit ihren wichtigsten Eigenschaften, nicht einen Eintrag je Molekül. Für das Lager sind das Artikel, Lagerort, Bestand und Bewegung. Ein Lagerort braucht eine Kennung, wie ein Regal in der Bibliothek. Ein Artikel braucht eine Nummer und eine Bezeichnung, mehr zunächst nicht. Die Kunst liegt in der Wahl der Eigenschaften: so genau, wie der Anwendungsfall es braucht, und nicht genauer. Mehr dazu im Hintergrundkapitel [Modellieren](../X-hintergrund/X020-modellieren.md).

**Die Bewegungen.** Der Bestand ändert sich nur über Bewegungen: Einlagern erhöht ihn, Auslagern senkt ihn. Niemand schreibt den Bestand direkt um. Das wirkt wie doppelte Buchführung, und es hat denselben Vorteil: Das Protokoll fällt als Liste der Bewegungen von selbst mit ab. Wer wissen will, wie ein Bestand zustande kam, liest die Bewegungen.

**Inaktiv statt gelöscht.** Was passiert mit einem Artikel, der nicht mehr geführt wird? Löschen macht das Protokoll wertlos, denn die alten Bewegungen zeigen dann ins Leere. Also bekommt der Artikel einen Zustand „inaktiv“. Es gibt ein Vorne und ein Hinten: Nach vorn ist der Artikel verschwunden, nach hinten bleibt alles nachvollziehbar.

**Klein schneiden.** Die erste Version ist ein Einzelplatz: ein Benutzer, ein einfaches Lager, Bedienung im Terminal. Eine Liste dessen, was unter dem Mindestbestand liegt, statt eines Bestellvorschlags. Freitext statt einer Verwaltung von Kategorien. Alles, was Sie jetzt weglassen, können Sie später hinzufügen. Alles, was Sie jetzt hineinnehmen, müssen Sie bauen, prüfen und pflegen.

## Gegen den Code-Impuls steuern

> **Der Agent treibt vorwärts, sein erster Impuls ist Code. Wann geredet wird, entscheiden Sie.**

Auch mitten im Gespräch wird der Agent anbieten, jetzt zu bauen. Lehnen Sie ab, solange Fragen offen sind. Sie müssen dafür nicht neu anfangen: Behalten Sie den Zwischenstand, lassen Sie den Agenten die bisherigen Anforderungen prüfen und die Lücken benennen. Eine gute Frage am Ende ist: „Sind die Anforderungen vollständig? Was fehlt dir noch?“ Was er nennt, füllen Sie selbst oder lassen es ihn erfragen.

Dann lassen Sie aufschreiben. Schlägt der Agent es nicht selbst vor, verlangen Sie es: eine Datei im Projektordner, etwa `Anforderungen.md`, in der alles steht, was Sie festgelegt haben. Das ist dieselbe Art Datei wie Ihre erste eigene aus dem Kapitel [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md). Lesen Sie sie. Es ist Ihre Datei, Sie dürfen hineinschreiben und danach mit dem Agenten weiter darüber reden. Diese Datei ist das erste Glied einer Kette, die das nächste Kapitel zeigt.

## Was jetzt klar sein sollte

- Der erste Satz entscheidet. „Programmieren“ ergibt Code, „Anforderungen entwickeln“ ergibt ein Gespräch. Sie sagen es im Prompt oder schalten den Planmodus ein.
- Der Agent stellt die Fachfragen und findet Randfälle, Sie entscheiden. Was Sie nicht sagen, füllt er mit dem Üblichen.
- Die Festlegungen für das Lager: ein Datenmodell aus Artikel, Lagerort, Bestand und Bewegung; der Bestand ändert sich nur über Bewegungen; inaktiv statt gelöscht; die erste Version klein.
- Am Ende steht eine Datei mit den Anforderungen im Projektordner, und erst dann kommt Code.

Weiter mit [Die Dokumentenkette](B020-die-dokumentenkette.md): Was auf die Anforderungen folgt und warum jeder Schritt ein eigenes Dokument bekommt.
