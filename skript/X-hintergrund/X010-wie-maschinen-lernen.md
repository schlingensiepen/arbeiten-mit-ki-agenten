# Wie Maschinen lernen

> **Stand der Quellen:** keine gebundene Quelle. Dieses Hintergrundkapitel stützt sich auf keine der öffentlichen Quellen des Skripts.

> **Eine KI ist im Kern ein Lineal, das so lange verschoben wird, bis der Fehler klein ist.**

Das Ganze ist halt n-dimensional mit n größer 1000, und der Fehler wird durch eine Loss-Function beschrieben. Wie man Minima bei Funktionen findet, haben Sie gefühlt die komplette Oberstufe in Mathe gemacht, und wie man das numerisch macht, ist anspruchsvoll, aber auch gelöst.

Im Kapitel [Was ein Agent ist](../A-verstehen-und-loslegen/A010-was-ein-agent-ist.md) heißt es, ein Sprachmodell sei ein trainiertes Modell. Dieses Kapitel erklärt das Wort „trainiert“. Es beginnt mit einem Lineal auf Papier, führt über Gewichte und Fehler zum Sprachmodell und endet bei der Frage, wie Reasoning entsteht. Formeln brauchen Sie dafür nicht. Das Kapitel ist Hintergrund: Der Rest des Skripts bleibt ohne es lesbar. Wer es gelesen hat, versteht aber, warum ein Modell nichts weiß wie ein Mensch, warum sein Wissen veraltet und was Reasoning ist und was nicht.

## Zwei Arten von Software

Klassische Software hat drei Teile: Eingabe, Verarbeitung, Ausgabe. Die Verarbeitung hat sich jemand ausgedacht. Ein Steuergerät im Auto bekommt Messwerte, rechnet nach einer Regel, die ein Ingenieur aufgeschrieben hat, und gibt einen Stellwert aus. Die Regel steht fest, bevor der erste Messwert kommt.

Gelernte Software dreht das um. Man steckt Vergangenheit hinein: Eingaben und die Ausgaben, die damals dazugehörten. Heraus kommen die Regeln. Niemand schreibt sie auf, sie entstehen aus den Beispielen. Dieses Entstehen ist das Lernen, und das Rechenzentrum, in dem es stattfindet, ist dabei nur Werkzeug, so wie ein Schraubendreher in einer Fabrik nicht erklärt, was die Fabrik tut. Wie Lernen geht, zeigt das einfachste Beispiel, das es gibt.

## Das Lineal

Ein Fahrzeug fährt eine Strecke. Zu sieben Zeitpunkten messen Sie, wie weit es gekommen ist, und tragen die Punkte auf Papier ein: Zeit nach rechts, Weg nach oben. Sie vermuten eine gleichmäßige Fahrt, also müsste eine Gerade durch die Punkte passen. Die Messung streut, deshalb liegt kein Punkt genau auf einer Geraden. Sie legen ein Lineal an, verschieben es, drehen es, bis es „passt“.

Was heißt passt? Für jeden Messpunkt gibt es einen Abstand zur Geraden. Dieser Abstand ist der Fehler des Punkts. Zählt man die Fehler aller Punkte zusammen, hat man den Gesamtfehler der Geraden. Die beste Gerade ist die mit dem kleinsten Gesamtfehler. Genau das tut Ihre Hand mit dem Lineal: Sie verschiebt es so lange, bis der Fehler klein ist.

![Ein Koordinatensystem mit der Achse Zeit nach rechts und der Achse Weg nach oben. Sieben grüne Messpunkte liegen verstreut um eine blaue Gerade. Von jedem Messpunkt führt ein kurzer oranger Strich senkrecht zur Geraden. Eine Legende benennt Messpunkt, Gerade und Fehler.](bilder/X010-lineal.svg)

**Die Gerade durch die Messpunkte.** Jeder Messpunkt hat einen Abstand zur Geraden, das ist sein Fehler. Gelernt ist die Gerade, bei der die Summe der Fehler am kleinsten ist.

Eine Gerade ist durch zwei Zahlen festgelegt: wo sie beginnt und wie steil sie ist. Lernen heißt, diese zwei Zahlen so zu wählen, dass der Gesamtfehler am kleinsten wird. Die Vorschrift, die zu zwei Zahlen den Gesamtfehler ausrechnet, heißt [Loss-Function](../Z-anhang/Z010-glossar.md#loss-function), Fehlerfunktion. Lernen ist die Suche nach ihrem Minimum. Wie man das Minimum einer Funktion findet, kennen Sie aus der Schule. Bei vielen Zahlen rechnet das ein Computer schrittweise aus; das ist anspruchsvoll, aber gelöst.

Ist die Gerade gefunden, bleibt sie fest. Jetzt können Sie für eine neue Zeit den Weg ablesen, auch für Zeiten, zu denen Sie nicht gemessen haben. Das Modell sagt voraus, auch über die Messpunkte hinaus.

Das Ergebnis des Lernens sind die zwei Zahlen. Sie heißen [Gewichte](../Z-anhang/Z010-glossar.md#gewichte). Mehr hat das Modell nicht gelernt, und mehr weiß es nicht. Das Gleiche macht eine KI.

## Mehr als zwei Zahlen: die Wahl-Hochrechnung

Am Wahlabend gibt es eine Hochrechnung, lange bevor alle Stimmen ausgezählt sind. Sie beruht auf einer Umfrage. Das Problem: Nicht alle antworten, und manche Gruppen antworten seltener als andere. Die Umfrage ist dadurch verzerrt. Die Lösung: Jede Gruppe bekommt ein Gewicht, und die Antworten werden gewichtet zusammengerechnet. Eine Gruppe, die selten antwortet, zählt stärker.

Woher kommen die Gewichte? Aus der Vergangenheit. Für frühere Wahlen sind Umfrage und Ergebnis bekannt. Man verschiebt die Gewichte so lange, bis die Hochrechnung der alten Wahlen deren Ergebnissen so nahe kommt wie möglich. Das ist dasselbe Lineal. Nur sind es nicht zwei Zahlen, sondern eine je Gruppe. Jedes Gewicht ist eine Richtung, in die man das Lineal schieben kann. Das ist gemeint, wenn es heißt, das Ganze sei n-dimensional. Vorstellen kann man sich das ab drei Richtungen nicht mehr. Rechnen kann man es trotzdem, das Verfahren bleibt gleich.

Dabei passiert ein Wechsel der Perspektive, der leicht übersehen wird. In der Formel der Hochrechnung sind die Umfragewerte die Eingabe und die Gewichte feste Zahlen. Beim Lernen ist es umgekehrt: Umfragewerte und Ergebnisse der alten Wahlen sind bekannt und fest, die Gewichte sind die Unbekannten. Die Gewichte werden zu Variablen. Ist das Lernen fertig, dreht sich die Perspektive zurück, und die Gewichte stehen fest. Viele Gewichte ordnet man in einer Tabelle an, einer Matrix. Mehr steckt hinter dem Wort nicht.

## Das Sprachmodell

Ein [Sprachmodell](../Z-anhang/Z010-glossar.md#llm) ist dieselbe Sache in groß. Die Eingabe ist Text, zerlegt in [Tokens](../Z-anhang/Z010-glossar.md#token), die Stücke, in die das Modell Text teilt. Die Ausgabe ist das wahrscheinliche nächste Token. Die Vergangenheit, aus der gelernt wird, ist sehr viel Text. Aus jedem Stück davon lässt sich ein Beispiel bilden, denn die richtige Fortsetzung steht ja da. Der Fehler ist, wie weit die Vorhersage neben dem tatsächlichen nächsten Token lag. Die Gewichte werden so lange verschoben, bis dieser Fehler über den gesamten Text klein ist. Gewichte gibt es jetzt nicht zwei, sondern bei heutigen Modellen weit mehr als tausend (Stand Oktober 2026).

Daraus folgt, was das Kapitel über Agenten nur festgestellt hat. Alles, was das Modell weiß, steckt in den Gewichten, und die stammen aus dem Text, der beim Training vorlag. Nach dem Training ändern sich die Gewichte nicht mehr. Deshalb veraltet das Wissen des Modells, und deshalb lernt ein Chatbot aus Ihrem Gespräch nichts dazu. Er wird nicht besser, er bekommt nur mehr [Kontext](../A-verstehen-und-loslegen/A020-kontext.md).

## Wie Reasoning entsteht

Ein fertiges Modell kann man weitertrainieren. Ein Spamfilter ist ein gelerntes Modell: Aus Beispielen für erwünschte und unerwünschte Post hat er gelernt, neue Post zu sortieren. Kommen neue Beispiele hinzu, werden seine Gewichte nachjustiert, nicht neu gelernt. Das Nachtrainieren geht vom fertigen Modell aus und verschiebt die Gewichte ein Stück weiter.

So entsteht [Reasoning](../Z-anhang/Z010-glossar.md#reasoning). Man nimmt ein fertiges Sprachmodell und stellt ihm Aufgaben, deren Ergebnis sich ohne eigene Intelligenz prüfen lässt: Logikaufgaben, oder die Aufgabe, ein Programm für die Fibonacci-Folge zu schreiben. Das Programm lässt man laufen und sieht, ob es stimmt. Richtig gibt eine Belohnung, falsch nicht. Aus dieser Prüfung wird die Fehlerfunktion, und die Gewichte werden nachjustiert. Heraus kommt ein Modell, das vor der Antwort Zwischenschritte aufschreibt und eine Aufgabe in Stufen löst, so wie es das Kapitel über Agenten beschreibt.

Das Wort Schlussfolgern trifft es nicht, auch wenn Reasoning so übersetzt wird. Das Modell schreibt weiterhin Text weiter. Es hat gelernt, welche Zwischenschritte zu Ergebnissen führen, die der Prüfung standhalten. Für den Agenten ist genau das die entscheidende Fähigkeit: Man kann das Modell jetzt statt nach der Antwort nach dem nächsten Schritt fragen, etwa danach, welches Tool es aufrufen würde.

## Was jetzt klar sein sollte

- Lernen heißt, Gewichte so lange zu verschieben, bis der Fehler klein ist. Die Fehlerfunktion misst den Fehler, Lernen sucht ihr Minimum.
- Die Gewichte sind alles, was ein Modell gelernt hat. Nach dem Training stehen sie fest. Deshalb veraltet das Wissen eines Modells, und deshalb lernt es aus Ihrem Gespräch nichts.
- Ein Sprachmodell ist dasselbe Verfahren in groß: Text hinein, nächstes Token heraus, nur mit sehr viel mehr Gewichten.
- Reasoning entsteht durch Nachtrainieren mit prüfbaren Aufgaben. Es bleibt Weiterschreiben, nur mit Zwischenschritten.

Zurück zu [Was ein Agent ist](../A-verstehen-und-loslegen/A010-was-ein-agent-ist.md).
