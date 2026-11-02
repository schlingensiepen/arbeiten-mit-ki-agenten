# Marken

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Staende-Freigaben-Marken.md`.

Im Kapitel [Die Dokumentenkette](../B-der-naive-ansatz/B020-die-dokumentenkette.md) haben Sie den naiven Ansatz gesehen: je Schritt ein Dokument, jedes baut auf dem vorigen auf, und das nächste wartet, bis das vorige fertig ist. In [Was man tun müsste](../C-der-langfristige-ansatz/C030-was-man-tun-muesste.md) stand als Folgerung: nach Marken schneiden statt nach Schritten, damit Arbeit nebeneinander laufen kann. Dieses Kapitel zeigt, was eine Marke ist, wie die Schritte aus Teil B dabei zu Phasen werden und warum aus der Kette ein Raster wird.

## Was eine Marke ist

Eine [Marke](../Z-anhang/Z010-glossar.md#marke) ist ein benanntes Ergebnis, das nach außen geht und freigegeben wird. Bei Software ist das ein Release, etwa „1.0“ oder „1.1“. Von außen sieht man von einem Projekt seine Marken und das, was sie liefern. Nach innen ordnet die Marke alles, was dazugehört: die Dokumente, ihre Freigaben, den Abschluss.

Drei Dinge ist eine Marke nicht. Sie ist kein Datum: Eine Frist kann zu einer Marke gehören, etwa ein zugesagter Liefertermin, aber sie ist nicht ihr Kern. Verstreicht die Frist, steht die Marke noch aus. Sie ist kein Meilenstein einer Zeitplanung: Gearbeitet wird fließend und nebeneinander. Und sie ist keine Arbeitseinheit: Eine Recherche oder ein Umbau im Inneren, der nichts nach außen liefert, gehört zur laufenden Marke. Eine neue Marke beginnt, wenn ein neues Ergebnis nach außen geht. Die Marke folgt dem Ergebnis, nicht dem Kalender.

Jedes Projekt führt Marken, von Anfang an. Der Agent legt beim Projektstart die erste an, die Bezeichnung nennen Sie. Im Regelfall ist eine Marke künftig, läuft oder ist abgeschlossen, und genau eine läuft. Im Regelwerk heißt die laufende Marke `in-progress`, in den Bildern dieses Skripts steht „läuft“.

Im Beispiel DONE heißt die erste Marke „1.0, Erster Release“, so steht es im Startprompt. Das ganze System besteht aus einem Backend und fünf Zugängen darauf. Alles auf einmal wäre eine sehr große erste Marke. In diesem Beispiel nehmen wir an, dass 1.0 das Backend und die Kommandozeile umfasst, denn damit lässt sich das Backend schon benutzen und prüfen. Die Mobile-App, die Desktop-App, der Server für Agenten und der Messenger-Bot kommen dann in späteren Marken, etwa 1.1 und 2.0. Das ist eine mögliche Antwort auf die Frage aus [Wer entscheidet was](../E-mensch-und-agent/E010-wer-entscheidet-was.md). Welcher Zugang wann kommt, ist eine Entscheidung von Ihnen, keine Ableitung.

## Phasen: Die Schritte bekommen einen Namen

Die Schritte aus der Dokumentenkette heißen im Regelwerk [Phasen](../Z-anhang/Z010-glossar.md#phase). Es sind dreizehn, jede nach ihrer Tätigkeit benannt, mit je einem Ergebnis:

| Phase | Tätigkeit |
|---|---|
| P1 | Konzipieren |
| P2 | Stand der Technik erfassen |
| P3 | Anforderungen sammeln |
| P4 | Beschreiben der Funktion |
| P5 | Zerlegen in Bausteine |
| P6 | Starten von Teilaktivitäten |
| P7 | Auswählen der Technologie |
| P8 | Spezifizieren |
| P9 | Ausarbeiten |
| P10 | Testen |
| P11 | Ausliefern |
| P12 | Produzieren |
| P13 | Betreiben |

Die Kette für die Lagerverwaltung aus Teil B finden Sie darin wieder: Die Anforderungen sind P3, die Spezifikation ist P8, die Implementierung P9, der Test P10; Datenmodell und Abläufe verteilen sich auf das Beschreiben der Funktion und das Zerlegen in Bausteine. Phasen heißen nach der Tätigkeit, „Zerlegen in Bausteine“ statt „Zerlegung“, weil die Tätigkeit sagt, was getan wird, während ein Substantiv offen lässt, ob Ergebnis oder Handlung gemeint ist.

Die Phasen sind ein Angebot, kein Zwang. Sie dürfen in beliebiger Reihenfolge arbeiten, eine Technologie ausprobieren, bevor die Bausteine feststehen, oder den Betrieb planen, bevor die Ausarbeitung fertig ist. Das Modell ist eine Checkliste: Der Agent fragt „Haben Sie das schon bedacht?“, und Sie antworten „ja, dort“, „nein, überspringen“ oder „machen wir jetzt“. Ein kleines Projekt lässt Phasen, die es nicht braucht, je Marke bewusst aus. Der Agent bucht das als [Verzicht](../Z-anhang/Z010-glossar.md#verzicht), damit das fehlende Dokument später nicht als Lücke gemeldet wird.

## Marken schneiden quer durch die Phasen

Jetzt kommen beide Begriffe zusammen. In der Dokumentenkette gab es je Schritt ein Dokument. Im langfristigen Ansatz gibt es je Marke und Phase eines: ein Dokument, das zusammenstellt, was zu dieser Marke in dieser Phase gilt, und das dann freigegeben wird. Das Skript nennt es [Freigabedokument](../Z-anhang/Z010-glossar.md#freigabedokument), das nächste Kapitel erklärt es genau. Im Regelwerk und in den Bildern heißt es kürzer Stand.

![Raster mit sieben der Phasen als Spalten, nämlich P3, P4, P5, P8, P9, P10 und P11, und den Marken 1.0, 1.1 und 2.0 als Zeilen. Marke 1.0 ist abgeschlossen und in allen Spalten gefüllt, die laufende Marke 1.1 ist bei P3, P4 und P5 gefüllt, die künftige Marke 2.0 ist leer.](bilder/F010-marken-raster.svg)

**Marken schneiden quer durch die Phasen.** Zu jeder Marke gehört je Phase ein eigener Stand, gezeigt sind sieben der dreizehn Phasen.

Lesen Sie das Bild zeilenweise. Marke 1.0 ist abgeschlossen: In jeder gezeigten Phase gibt es ein freigegebenes Dokument, Backend und Kommandozeile sind ausgeliefert. Marke 1.1 läuft: Zu P3, P4 und P5 gibt es freigegebene Dokumente, also Anforderungen, Funktionsbeschreibung und Architektur. Ab P8 sind die Kreise leer, dort gibt es noch kein Dokument. Marke 2.0 ist künftig und hat noch kein Dokument. Lesen Sie es spaltenweise, sehen Sie die Dokumentenkette wieder, aber je Marke einmal: Die Anforderungen zu 1.1 sind ein anderes Dokument als die zu 1.0.

Ein Dokument zu einer Marke beschreibt dabei immer das Ganze, nicht nur den Zuwachs. Die Funktionsbeschreibung zu 1.1 enthält also auch, was aus 1.0 weiter gilt. Was sich seit 1.0 nicht geändert hat, muss trotzdem nicht neu erarbeitet werden: Ein freigegebenes Dokument der Vormarke gilt für die nächste Marke weiter, solange nichts darin überholt ist.

## Warum das Arbeit nebeneinander erlaubt

In der Kette wartet jeder Schritt auf den vorigen, und solange die Implementierung läuft, liegen die Anforderungen still. Im Raster nicht. Jedes [Element](../Z-anhang/Z010-glossar.md#element) eines [Registers](../Z-anhang/Z010-glossar.md#register), etwa eine Anforderung, trägt die Marke, zu der es gehört. Beim Anlegen bekommt es die laufende Marke; ist es für später geplant, die spätere. Eine Anforderung für 2.0 darf also entstehen und angenommen werden, während es zu 1.1 noch keine Spezifikation gibt. Sie gehört einfach in eine andere Zeile des Rasters. Geordnet ist nur, in welcher Reihenfolge die Freigabedokumente einer Marke freigegeben werden; dazu mehr in [Freigabe von x für y](F030-freigabe-von-x-fuer-y.md).

Das ist auch der Grund, warum im Kapitel [Register und Elemente](../D-wissen-im-wiki/D040-register-und-elemente.md) nichts gelöscht, sondern abgelöst wird. Löst eine Anforderung mit Marke 2.0 eine ältere ab, gilt die alte für 1.0 und 1.1 weiter und die neue ab 2.0. Die Funktionsbeschreibung zu 1.1 bleibt dadurch richtig, obwohl für 2.0 schon etwas anderes gewünscht ist.

## Wenn eine Marke fertig ist

Ist eine Marke am Ende, schließt der Agent sie in festen Schritten ab. Er legt Ihnen vor, was zu ihr noch offen ist, und Sie entscheiden je Punkt: jetzt erledigen oder auf eine spätere Marke verschieben. Dann bildet er ein letztes Dokument, das alle freigegebenen Dokumente der Marke aufzählt, Sie geben es frei, und die Marke wechselt auf abgeschlossen. Ab da ist sie [eingefroren](../Z-anhang/Z010-glossar.md#einfrieren): Was zu 1.0 gehört, ändert sich nicht mehr. Die nächste Marke läuft. Den ganzen Weg einer Marke von der ersten Anforderung bis zur Auslieferung zeigt [Softwareentwicklung als Prozess](../G-der-gesamtprozess/G010-softwareentwicklung-als-prozess.md).

## Was jetzt klar sein sollte

- Eine Marke ist ein benanntes Ergebnis, das nach außen geht, etwa ein Release. Kein Datum, kein Meilenstein.
- Phase ist das Wort des Regelwerks für die Schritte aus der Dokumentenkette. Phasen sind ein Angebot, eine Checkliste.
- Je Marke und Phase gibt es ein eigenes Freigabedokument. Aus der Kette wird ein Raster.
- Jedes Element trägt seine Marke. Deshalb kann an 2.0 gearbeitet werden, während 1.1 läuft.
- Eine abgeschlossene Marke ist eingefroren.

Weiter mit [Freigabedokument: Sammler und Freezer](F020-freigabedokument-sammler-und-freezer.md): Was in einem Freigabedokument steht und warum es einfriert.
