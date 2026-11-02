# Aufpasser-Modelle

> **Stand der Quellen:** keine gebundene Quelle. Dieses Hintergrundkapitel stützt sich auf keine der öffentlichen Quellen des Skripts.

Im Kapitel [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md) steht, dass Sie [Skip Permissions](../Z-anhang/Z010-glossar.md#skip-permissions) nur auf einem wegwerfbaren Rechner verwenden. Einer der Gründe ist dort nur angedeutet: Die Schutzeinrichtung beim Anbieter ist nur eine zweite Linie. Dieses Kapitel erklärt, was man über diese Schutzeinrichtung hört und warum Sie sich nicht auf sie verlassen.

Vorweg zur Herkunft. Alles, was dieses Kapitel über das Innere der Anbieter sagt, stammt aus Gesprächen mit Leuten, die dort arbeiten. Die Firmen selbst halten sich bedeckt, weil es um Firmengeheimnisse geht. Offiziell bestätigt ist nichts davon, einen öffentlichen Beleg gibt es nicht, und kein Anbieter wird hier genannt. Lesen Sie die folgenden Abschnitte als das, was man aus der Branche hört, Stand Oktober 2026.

## Ein Modell passt auf das andere auf

Was man hört, ist dies: Beim Anbieter läuft nicht nur das Sprachmodell, mit dem Sie reden. Ein zweites Modell liest mit, was das erste antwortet, und hält zurück, was nicht hinaus soll, etwa einen wilden Löschbefehl, der als [Tool-Aufruf](../Z-anhang/Z010-glossar.md#tool-aufruf) an Ihren Rechner zurückkäme. Das Skript nennt dieses zweite Modell [Aufpasser-Modell](../Z-anhang/Z010-glossar.md#aufpasser-modell). Die Antwort, die Sie sehen, wäre demnach schon einmal gesiebt, bevor sie Ihren Harness erreicht.

## Rohe Modelle als Gegenbild

Wie sich ein Modell ohne alles, was um es herum gebaut ist, verhält, zeigen rohe Modelle, und auch darüber hört man nur. Sie liefern nicht zuverlässig, was man bestellt. Ein Beispiel ist JSON, ein festes Textformat für Daten, das ein Programm weiterverarbeiten soll. Bittet man ein rohes Modell um JSON, kommt nicht jedes Mal welches. Was Sie als Produkt erleben, ist also nicht das rohe Modell. Wie ordentlich eine Antwort wirkt, sagt wenig darüber, was das Modell von sich aus täte.

## Zahlen, mit Vorsicht

Man hört auch Zahlen, Stand Oktober 2026: Von 64 Grafikkarten, den Rechenbausteinen, auf denen solche Modelle laufen, rechnen 40 mit dem eigentlichen Modell. Der Rest passt auf. Stimmt das, geht ein gutes Drittel der Rechenleistung nicht in die Antwort, sondern in die Aufsicht. Nehmen Sie die Zahl als das, was sie ist: Hörensagen. Niemand außerhalb der Firmen kann sie prüfen, und sie kann morgen anders sein.

## Alles im Fluss

Dass sie morgen anders sein kann, hat einen konkreten Grund. Experten in einem Sprachmodell sind Teilnetze, von denen je Anfrage nur ein Teil arbeitet. Heute hat das Modell alle Experten im Zugriff, nutzt aber nicht alle. Eine nächste Generation könnte aus dem Prompt vorhersagen, welche Experten gebraucht werden, und dann andere Instanzen aufrufen. Damit können sich die Verhältnisse ändern: wie viel Rechenleistung in das Modell geht, wie viel in die Aufsicht, und was überhaupt eine Instanz des Modells ist. Die Zahlen von oben beschreiben einen Augenblick, keine Regel.

## Was das für Sie heißt

Der Aufpasser ist eine zweite Linie, und sie liegt hinter Ihrer. Ihre erste Linie ist die [Berechtigungsstufe](../Z-anhang/Z010-glossar.md#berechtigungsstufe) Ihres Agenten: Der [Harness](../Z-anhang/Z010-glossar.md#harness) fragt, bevor er einen Befehl ausführt, und Sie entscheiden. Skip Permissions streicht diese Linie. Dann bleibt nur die zweite, und über die wissen Sie nur, was man hört. Nicht, ob es sie bei Ihrem Anbieter gibt. Nicht, wie sie eingestellt ist. Nicht, ob sie morgen noch so arbeitet wie heute. Eine Schutzeinrichtung, die Sie weder sehen noch prüfen noch einstellen können, ist keine, auf die Sie sich verlassen. Deshalb gilt: Skip Permissions nur auf einem wegwerfbaren Rechner ohne wertvolle Zugänge oder Daten, und nur, wenn die Arbeit per Git gesichert ist.

## Was jetzt klar sein sollte

- Beim Anbieter passt nach dem, was man aus der Branche hört, ein zweites Modell auf das erste auf. Offiziell bestätigt ist das nicht.
- Rohe Modelle zeigen, was ein Modell ohne diese Zutaten täte: Sie liefern nicht zuverlässig, was man bestellt.
- Die Zahlen dazu sind Hörensagen mit Stand Oktober 2026, und sie sind im Fluss, weil sich der Aufbau der Modelle ändert.
- Ihre Berechtigungsstufe ist die erste Linie. Wer sie streicht, verlässt sich auf eine Einrichtung, die er weder sehen noch prüfen kann.

Zurück zu [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md).
