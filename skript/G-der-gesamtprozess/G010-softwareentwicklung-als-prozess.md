# Softwareentwicklung als Prozess

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `Vorgehen.md`, `docs/Referenzprozesse.md`, `wiki/Vorgehen-RP-1.md`, `wiki/Kettenpruefung.md`.

> **Software ist am Ende auch nur ein Produkt. Es gibt keinen Grund, sie anders zu entwickeln.**

In den letzten Kapiteln haben Sie Einzelteile kennengelernt: das Wiki mit seinen Registern, die Marke als Zwischenziel, das Freigabedokument, die Freigabe für einen Zweck. Dieses Kapitel setzt die Teile zusammen. Das Ergebnis ist das, was das Regelwerk einen Prozess nennt: eine Folge von Phasen, von denen jede ein Freigabedokument hervorbringt, und eine Prüfung, die jedes dieser Dokumente vor seiner Freigabe gegen die früheren hält. Der Kern dieses Fachs ist das Beschreiben: was das Problem ist, was die Software können soll, wie sie aufgebaut ist. Der Code ist, was am Ende aus den Beschreibungen wird. Wer den Prozess verstanden hat, weiß, in welcher Reihenfolge die Freigaben kommen, warum der Agent vor jeder Freigabe zurückschaut und was die erste Marke eines Projekts von Anfang bis Ende durchläuft.

## Ein Produkt entsteht in Schritten

Nehmen Sie etwas, das Sie selbst schon gebaut haben, etwa ein Regal für eine bestimmte Nische. Sie messen zuerst die Nische aus und überlegen, was hineinsoll. Dann zerlegen Sie das Regal im Kopf in Böden, Seiten und Verbinder, wählen Holz und Schrauben, zeichnen den Zuschnitt. Erst dann wird gesägt und geschraubt. Danach prüfen Sie, ob das Regal steht und trägt, und stellen es auf. Niemand sägt zuerst und misst danach.

Bei Software ist das nicht anders, nur dass man die frühen Schritte leichter überspringt. Ein Agent schreibt auf Zuruf sofort Code, und Code sieht nach Fortschritt aus. Teil B hat gezeigt, wohin das führt. Der Prozess in diesem Kapitel ist die Antwort darauf: dieselben Schritte wie beim Regal, mit festen Namen und einem festen Ergebnis je Schritt.

## Die Phasen

Das Regelwerk teilt die Arbeit in dreizehn [Phasen](../Z-anhang/Z010-glossar.md#phase). Jede Phase ist als Tätigkeit benannt, nicht als Zustand: „Anforderungen sammeln“, nicht „Anforderungsanalyse“. So ist klar, dass jemand etwas tut. Jede Phase hat ein Ergebnis, und das Ergebnis ist ein Dokument, das freigegeben werden kann. Die Phasen tragen das Präfix P und eine Nummer.

| Phase | Tätigkeit | Ergebnis |
|---|---|---|
| P1 | Konzipieren | Konzept |
| P2 | Stand der Technik erfassen | Bericht zum Stand der Technik |
| P3 | Anforderungen sammeln | Anforderungen |
| P4 | Beschreiben der Funktion | Funktionsbeschreibung |
| P5 | Zerlegen in Bausteine | Architektur |
| P6 | Starten von Teilaktivitäten | Verweise auf die Teil-Projekte |
| P7 | Auswählen der Technologie | Technologie-Entscheidungen |
| P8 | Spezifizieren | Spezifikation, die Bauanleitung |
| P9 | Ausarbeiten | das Produkt selbst |
| P10 | Testen | Testplan und Testbericht |
| P11 | Ausliefern | Beschreibung der Auslieferung je Umgebung |
| P12 | Produzieren | Bereitstellen der Umgebung |
| P13 | Betreiben | Betriebs-Handbuch |

Diese Liste ist absichtlich nicht auf Software gemünzt. Die Vorlage, mit der Sie arbeiten, hat einen neutralen Kern, und ein [Referenzprozess](../Z-anhang/Z010-glossar.md#referenzprozess) belegt die Phasen für eine Projektart. Der Prozess für Softwareentwicklung, der in der Vorlage schon eingespielt ist, belegt sie so: Das Produkt aus P9 ist der Code mit seinen automatisierten Tests, die Spezifikation aus P8 ist so genau, dass sie ohne Fachwissen umsetzbar ist, und die Auslieferung aus P11 beschreibt je Zielumgebung, was ausgerollt wird. Andere Projektarten gibt es in der Vorlage als Steckbrief, etwa Rechtsfall, Publikation oder Hardwareentwicklung; sie sind zum Zeitpunkt dieses Skripts geplant, nicht ausgearbeitet (Stand Oktober 2026). Das ist der Punkt des Satzes am Anfang: Die Schritte sind dieselben, ob am Ende Code, ein Schriftsatz oder ein Gerät herauskommt.

Die Phasen sind ein Angebot, kein Zwang. Sie dürfen in beliebiger Reihenfolge an ihnen arbeiten, etwa während der Architektur schon eine Technologie ausprobieren. Der Agent benutzt die Liste als Checkliste. Bei jedem Anlass fragt er: Haben Sie das schon bedacht? Darauf gibt es drei Antworten: Ja, das steht dort und dort, dann legt der Agent das Ergebnis mit dem Verweis ab. Nein, überspringen, dann vermerkt er die Phase als bewusst ausgelassen. Oder: Ja, machen wir jetzt.

## Phasen ordnen Freigaben, nicht Arbeit

Dieser Satz aus dem Kapitel [Freigabe von x für y](../F-marken-und-freigaben/F030-freigabe-von-x-fuer-y.md) ist der Schlüssel zum ganzen Prozess. Das Regelwerk kennt zwei Ordnungen, und sie sind verschieden.

Die Erarbeitung der [Elemente](../Z-anhang/Z010-glossar.md#element) ist ungeordnet. Eine Anforderung, eine Entscheidung, ein Testfall darf jederzeit entstehen und angenommen werden, sobald Sie es wissen. Eine Technologie-Entscheidung kann im Register stehen, bevor die Funktion fertig beschrieben ist. Die Phase ist kein Merkmal eines Elements.

Die Freigabe der [Freigabedokumente](../Z-anhang/Z010-glossar.md#freigabedokument) ist geordnet. Das Dokument einer Phase wird nach den Dokumenten der früheren Phasen derselben [Marke](../Z-anhang/Z010-glossar.md#marke) freigegeben. Jede [Freigabe](../Z-anhang/Z010-glossar.md#freigabe) nennt dabei ihren Zweck, und der Zweck ist die nächste Phase: Die Anforderungen werden freigegeben „für P4 Beschreiben der Funktion“, die Funktionsbeschreibung „für P5 Zerlegen in Bausteine“, die Spezifikation „für P9 Ausarbeiten“. Das Dokument, auf das Sie sich in der nächsten Phase stützen, steht damit fest, bevor die nächste Phase beginnt.

Fehlt ein früheres Dokument, etwa weil niemand die Architektur aufgeschrieben hat, blockiert der Agent nicht. Er warnt bei der nächsten Freigabe, und Sie entscheiden. Geben Sie trotzdem frei, nennt der Eintrag der Freigabe den fehlenden Vorgänger als Einschränkung. Eine Ausnahme gibt es: Der Testplan wird erst nach dem Tag freigegeben. Was der Tag ist, kommt jetzt.

## Der Tag: das Produkt in der Kette

Die Phase P9, das Ausarbeiten, fällt aus der Reihe. Ihr Ergebnis ist kein Dokument, sondern das Produkt: bei Software der Code mit seinen Tests. Ein Produkt kann man nicht wie ein Dokument einfrieren und ablegen. Dafür gibt es in [Git](../Z-anhang/Z010-glossar.md#git) den Tag: eine Markierung an einem bestimmten [Commit](../Z-anhang/Z010-glossar.md#commit), die einen Namen trägt. Der Agent setzt den Tag nach Ihrem OK in dem Repo, das den Code trägt. Vorbedingung ist, dass die automatisierten Tests grün sind. Der Name des Tags folgt einer Konvention, die im Wiki festgehalten ist; er ist nicht die Bezeichnung der Marke. Die Marke heißt „1.1“, der Tag kann „v1.1.0“ heißen.

Ein gesetzter Tag wird nie verschoben und nie gelöscht. Muss der Code korrigiert werden, entsteht ein neuer Tag mit einer neuen Freigabe, und die alte wird abgelöst. Das ist dieselbe Regel wie bei den Freigabedokumenten: Was einmal fest ist, bleibt fest; Änderungen kommen als Nachfolger dazu.

## Die Prüfkette

Die Freigabedokumente einer Marke bilden mit dem Tag eine Reihe, in der jedes Glied auf den vorigen aufbaut. Das Skript nennt diese Reihe [Prüfkette](../Z-anhang/Z010-glossar.md#prüfkette), weil vor jeder Freigabe geprüft wird, ob das neue Glied zu den alten passt. Das Regelwerk sagt kürzer Kette und nennt die einzelne Prüfung Kettenprüfung.

Die Regel: Jedes Dokument wird vor seiner Freigabe gegen alle freigegebenen Vorgänger derselben Marke geprüft, nicht nur gegen den direkten Vorgänger. Geprüft wird auf drei Dinge:

- **Widerspruch:** Das Dokument widerspricht einem Vorgänger. Die Spezifikation sieht ein Feld vor, das die Funktionsbeschreibung ausschließt.
- **Abdeckung:** Alles aus den Vorgängern ist aufgegriffen. Jede Anforderung findet sich in der Funktionsbeschreibung wieder.
- **Unbegründetes:** Inhalt, den kein Vorgänger trägt. Die Architektur enthält einen Baustein, für den es keine Anforderung gibt.

Einen Teil dieser Prüfung erledigt ein Programm, einen Teil ein Prüfer mit frischem Kontext. Wie beides geht und warum der Prüfer ein zweites Modell sein soll, ist das Thema des nächsten Kapitels. Hier genügt: Das Ergebnis ist ein Prüfbericht, und die Freigabe verweist auf ihn.

Die Kette wirkt auch rückwärts. Fällt beim Spezifizieren auf, dass eine Anforderung nicht haltbar ist, wird nicht die Spezifikation verbogen. Die Anforderung wird durch ein neues Element abgelöst, das Freigabedokument der Anforderungen ist damit überholt und wird neu gebildet, so wie es das Kapitel [Freigabedokument: Sammler und Freezer](../F-marken-und-freigaben/F020-freigabedokument-sammler-und-freezer.md) beschreibt. Die Kette bleibt in sich stimmig, weil nichts an ihr vorbei geändert wird.

![Ein grauer Container mit der Beschriftung Marke 1.0. Darin sieben Spalten von links nach rechts: Anforderungen sammeln, Beschreiben der Funktion, Zerlegen in Bausteine, Spezifizieren, Ausarbeiten, Testen, Ausliefern. Unter jeder Phase ein blauer Block mit ihrem Freigabedokument und der Phasennummer: Anforderungen P3, Funktionsbeschreibung P4, Architektur P5, Spezifikation P8, Testplan P10, Auslieferung P11; unter Ausarbeiten statt eines Blocks ein blauer Kreis mit der Aufschrift Tag P9. Eine schwarze Linie mit Pfeilspitze verbindet alle Glieder nach rechts. Drei orange Pfeile führen von der Spezifikation zurück zu Architektur, Funktionsbeschreibung und Anforderungen, daneben steht: vor der Freigabe geprüft gegen alle freigegebenen Vorgänger.](bilder/G010-phasenkette.svg)

**Phasen und Prüfkette.** Jede Phase endet in einem Freigabedokument, das Ausarbeiten im Tag auf dem Code. Die Freigaben laufen von links nach rechts; vor jeder Freigabe prüft der Agent das neue Glied gegen alle, die davor schon freigegeben sind, hier die Spezifikation gegen Architektur, Funktionsbeschreibung und Anforderungen. Das Bild zeigt sieben der dreizehn Phasen; Konzipieren, Stand der Technik, Starten von Teilaktivitäten, Auswählen der Technologie, Produzieren und Betreiben fehlen, damit es lesbar bleibt.

## Beispiel: Die erste Marke von DONE

Beim Aufsetzen von DONE hieß die erste Marke „1.0, Erster Release“. Sie umfasst das Backend und die Kommandozeile. So läuft sie durch die Phasen:

1. **Anforderungen sammeln.** Im Gespräch entstehen Anforderungen und werden als Elemente angenommen: TODOs haben Sub-TODOs und Abhängigkeiten, was keinen Tag hat, liegt in der Inbox, TODOs lassen sich delegieren. Der Agent bildet das Freigabedokument der Anforderungen zur Marke 1.0. Es wird geprüft und freigegeben „für P4 Beschreiben der Funktion“.
2. **Beschreiben der Funktion.** Aus den Anforderungen wird eine geschlossene Beschreibung, was DONE aus Sicht des Benutzers tut. Vor der Freigabe prüft der Agent sie gegen die Anforderungen: Ist jede aufgegriffen, widerspricht nichts, steht nichts darin, was keine Anforderung trägt?
3. **Zerlegen in Bausteine.** Die Architektur nennt das Backend mit seiner Schnittstelle und die Kommandozeile als Bausteine. Geprüft gegen Anforderungen und Funktionsbeschreibung.
4. **Spezifizieren.** Die Bauanleitung, so genau, dass sie ohne Fachwissen umsetzbar ist, auch von einem weiteren Agenten. Geprüft gegen alle drei Vorgänger.
5. **Ausarbeiten.** Der Agent schreibt Code und Tests. Sind die Tests grün, setzt er nach Ihrem OK den Tag.
6. **Testen.** Der Testplan enthält, was sich nicht automatisieren lässt, etwa Ihren eigenen Durchgang durch die Kommandozeile. Er wird erst nach dem Tag freigegeben; das Ergebnis ist ein Testbericht.
7. **Ausliefern.** Die Beschreibung, wie DONE auf eine Zielumgebung kommt.

Zum Schluss bildet der Agent ein letztes Freigabedokument, das die Marke abschließt und alle Glieder nennt. Mit seiner Freigabe ist die Marke 1.0 abgeschlossen und eingefroren, und die nächste Marke beginnt, etwa mit einem weiteren Zugang zu DONE. Dafür wird nicht alles neu gebildet: Ein Freigabedokument aus der Marke 1.0, das weiter gilt, gilt auch für die Marke 1.1, solange es nicht überholt ist.

## Was jetzt klar sein sollte

- Der Prozess besteht aus Phasen, jede als Tätigkeit benannt, jede mit einem Freigabedokument als Ergebnis. Die Phasen sind ein Angebot und eine Checkliste, kein Zwang.
- Die Phasen ordnen die Freigaben, nicht die Arbeit: Elemente entstehen jederzeit, Freigabedokumente werden der Reihe nach freigegeben, jedes für den Zweck der nächsten Phase.
- Das Produkt selbst, bei Software der Code, wird nicht als Dokument eingefroren, sondern mit einem Tag markiert. Ein Tag wird nie verschoben.
- Die Prüfkette: Vor jeder Freigabe wird das neue Glied gegen alle freigegebenen Vorgänger derselben Marke geprüft, auf Widerspruch, Abdeckung und Unbegründetes.

Weiter mit [Prüfen](G020-pruefen.md): Wer prüft, warum ein zweites Modell darauf schaut und was ein Programm ohne Modell vorher erledigt.
