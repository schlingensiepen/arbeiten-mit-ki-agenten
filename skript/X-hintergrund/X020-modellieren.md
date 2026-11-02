# Modellieren

> **Stand der Quellen:** keine gebundene Quelle. Dieses Hintergrundkapitel stützt sich auf keine der öffentlichen Quellen des Skripts.

> **Software bildet die Realität ab, und zwar nur so genau, wie der Anwendungsfall es braucht.**

Im Kapitel [Anforderungen im Gespräch](../B-der-naive-ansatz/B010-anforderungen-im-gespraech.md) fragt der Agent nach Lagerorten, Artikeln und Beständen, und Sie entscheiden. Hinter diesen Fragen steckt eine Tätigkeit, die älter ist als jeder Agent: das Modellieren. Dieses Kapitel erklärt, was ein Modell ist, warum es nie vollständig ist und woran Sie erkennen, was hineingehört und was nicht. Es ist Hintergrund: Der Rest des Skripts bleibt ohne es lesbar. Wer es gelesen hat, versteht die Fragen des Agenten besser und weiß, was eine gute Antwort darauf ausmacht.

## Was ein Modell ist

Ein Lager besteht aus Regalen, Fächern, Kisten und Artikeln. Jeder Artikel hat unzählige Eigenschaften: eine Nummer, eine Bezeichnung, eine Farbe, eine Form, ein Material, ein Gewicht, eine Herkunft. Kein Programm kann das alles aufnehmen, und keines soll es. Software bildet einen Ausschnitt der Realität ab. Diesen Ausschnitt nennt man Modell. Die Lagerverwaltung dieses Skripts braucht zum Beispiel nur ein Wort für jede Stelle, an der etwas liegen kann, ob Regal, Fach oder Kiste: den Lagerort.

Die Funktionen eines Programms sind die Knöpfe, mit denen man dieses Modell verändert. Einlagern erhöht den Bestand, Entnehmen senkt ihn, Umlagern ändert den Lagerort. Das Modell steht für die Realität, es ist nicht die Realität. Ob es taugt, entscheidet sich an einer Frage: Ist es für den Anwendungsfall genau genug?

## Attribute: die Kunst der Auswahl

Die Eigenschaften, die ins Modell aufgenommen werden, heißen Attribute. Die Kunst des Modellierens liegt in ihrer Wahl, und der Maßstab ist der Anwendungsfall. Für die Lagerverwaltung reicht die Artikelnummer, um einen Artikel zu erkennen. Die Farbe braucht das Modell nur, wenn jemand im Lager nach Farbe sucht. Wer sie trotzdem aufnimmt, macht das Modell nicht besser, sondern nur größer: Jedes Attribut muss erfasst, gepflegt und angezeigt werden.

![Links ein grauer Container mit der Beschriftung Lager, Realität. Darin ein grüner Block Artikel mit den Eigenschaften Artikelnummer, Bezeichnung, Bestand, Farbe, Form, Material und drei Punkten. Ein oranger Pfeil mit der Beschriftung Auswahl der Attribute führt nach rechts in einen grauen Container Modell. Darin ein blauer Block Artikel mit den drei Attributen Artikelnummer, Bezeichnung und Bestand. Darunter drei gestrichelte graue Kästen Farbe, Form und Material mit der Beschriftung bleibt draußen.](bilder/X020-modell-der-realitaet.svg)

**Das Lager und sein Modell.** Von den vielen Eigenschaften eines Artikels nimmt das Modell nur die auf, die der Anwendungsfall braucht. Alles andere bleibt draußen.

Wie genau ein Attribut sein muss, ist dieselbe Frage eine Stufe tiefer. Zwei Beispiele aus dem Gespräch über die Lagerverwaltung:

- Wird der Bestand in Packungen gezählt oder in Gramm gewogen? Das ist eine fachliche Frage mit einer technischen Folge: Packungen bucht man von Hand, für Gramm schließt man eine Waage an.
- Werden Gramm als ganze Zahl gespeichert oder mit Nachkommastellen? Ganze Zahlen reichen, und Kommazahlen machen beim Eingeben Ärger.

Beide Entscheidungen legen fest, wie genau das Modell ist. Genauer als nötig ist nicht besser, es ist nur teurer.

Dazu gehört, klein anzufangen. Ein Einzelplatz statt vieler Benutzer, ein einfaches Lager, eine Liste statt eines Bestellvorschlags, ein Freitext statt einer Kategorienverwaltung. Ein Modell darf wachsen. Es muss nicht am ersten Tag alles enthalten, was das Lager irgendwann einmal brauchen könnte.

## Was passieren kann: Beziehungen und Anzahlen

Attribute allein reichen nicht. Die Dinge im Modell hängen zusammen: Ein Artikel liegt an einem Lagerort. Nur, an wie vielen? Die Frage, die das klärt, lautet: Was kann passieren? Tausend Pakete Taschentücher passen nicht in ein Fach. Ein Artikel könnte also mehrere Lagerorte brauchen. Die Lagerverwaltung dieses Skripts bleibt klein und legt fest: ein Lagerort je Artikel. Kann ein Lagerort umgekehrt mehrere Artikel enthalten? Das entscheidet wieder der Anwendungsfall. Solche Anzahlen heißen Kardinalitäten: eins oder viele, auf jeder Seite einer Beziehung. Der Agent fragt danach, weil das Programm sonst beim ersten Sonderfall bricht.

## Datenmodell und Metamodell

Beim Modellieren entstehen zwei Ebenen. Die eine ist das konkrete Lager mit seinen Daten: Artikel 4711, Bestand zwölf, Lagerort B3. Die andere ist die Festlegung darüber, welche Arten von Dingen es gibt und welche Attribute und Beziehungen jede Art hat: Ein Artikel hat eine Artikelnummer, eine Bezeichnung und einen Bestand und liegt an genau einem Lagerort. Diese zweite Ebene heißt [Datenmodell](../Z-anhang/Z010-glossar.md#datenmodell).

Im Gespräch mit dem Agenten über die Anforderungen entsteht genau dieses Datenmodell. Die Daten kommen später, wenn das Programm läuft. Was Sie im Gespräch entscheiden, legt also fest, was das Programm überhaupt aufnehmen kann.

Eine Ebene höher liegt das [Metamodell](../Z-anhang/Z010-glossar.md#metamodell), das Modell des Modells. Es legt fest, woraus ein Datenmodell bestehen kann: aus Arten von Dingen, ihren Attributen und ihren Beziehungen.

## Was jetzt klar sein sollte

- Software bildet einen Ausschnitt der Realität ab. Dieser Ausschnitt ist das Modell, die Funktionen sind die Knöpfe daran.
- Welche Attribute hineinkommen und wie genau sie sind, entscheidet der Anwendungsfall. Nicht genauer als nötig.
- Beziehungen und ihre Anzahlen findet man mit der Frage, was passieren kann.
- Das Datenmodell legt die Arten, Attribute und Beziehungen fest. Es entsteht im Gespräch über die Anforderungen, die Daten kommen später. Das Metamodell liegt eine Ebene höher und sagt, woraus ein Datenmodell bestehen kann.

Zurück zu [Anforderungen im Gespräch](../B-der-naive-ansatz/B010-anforderungen-im-gespraech.md). Das Beispiel zum Nachmachen steht unter [Lagerverwaltung](../Y-beispiele/Y010-lagerverwaltung.md).
