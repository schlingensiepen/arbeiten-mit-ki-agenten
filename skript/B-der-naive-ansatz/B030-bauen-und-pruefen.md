# Bauen und prüfen

> **Stand der Quellen:** keine gebundene Quelle. Dieses Kapitel beschreibt kein Werkzeug, sondern einen Arbeitsschritt.

Die Kette aus dem vorigen Kapitel liegt als Dateien im Projektordner, bis zur Spezifikation: `anforderungen.md`, `datenmodell-und-ablaeufe.md` und `spezifikation.md`. Jetzt kommt der Schritt, für den viele den Agenten überhaupt wollen: Er soll bauen. Dieses Kapitel zeigt, wie Sie bauen lassen, wie Sie das Ergebnis lesen, ohne die Programmiersprache zu können, was das Ihr Kontextfenster kostet, und warum die Prüfung am Ende trotzdem bei Ihnen bleibt.

## Bauen lassen

Der Auftrag ist kurz, denn die Arbeit steckt schon in den Dokumenten:

```text
Implementiere die Lagerverwaltung nach der Spezifikation in spezifikation.md. Halte dich an das Datenmodell und die Abläufe aus datenmodell-und-ablaeufe.md.
```

Die Programmiersprache können Sie frei wählen oder dem Agenten überlassen. Ein guter Kandidat ist Java, weil Java die Strukturen des Datenmodells im Quelltext gut sichtbar macht. In der ersten Runde muss niemand Java können. Das ist der Grund für die Reihenfolge, die dieser Teil einhält: Lesen ist leicht, selbst programmieren ist viel aufwendiger. Also erst die Anforderungen, dann ausprogrammieren lassen, dann lesen.

Was jetzt passiert, kennen Sie aus dem Kapitel [Was ein Agent ist](../A-verstehen-und-loslegen/A010-was-ein-agent-ist.md): Der Agent arbeitet viele Runden, ohne dass Sie etwas tun. Er legt Ordner und Dateien an, schreibt Quelltext, führt Befehle aus, liest Fehlermeldungen, bessert nach. Je nach [Berechtigungsstufe](../Z-anhang/Z010-glossar.md#berechtigungsstufe) fragt er vor Befehlen nach. Nach einigen Minuten meldet er, dass er fertig ist.

## Das Ergebnis lesen

Jetzt steht in Ihrem Projektordner ein Programm, geschrieben in einer Sprache, die Sie nicht können. Sie können es trotzdem lesen, denn Sie kennen die Dokumente, aus denen es entstanden ist. Lesen heißt hier: den Aufbau gegen die Dokumente halten.

- **Der Aufbau.** Das Ergebnis gliedert sich in die Fachlogik und die Bedienoberfläche. Die Fachlogik ist das, was im Datenmodell und in den Abläufen steht: Artikel, Lagerort, Bestand, Bewegung, Einlagern, Auslagern. Die Bedienoberfläche ist hier eine Textoberfläche im Terminal, die diese Abläufe aufruft. Oft hat der Agent dafür zwei Ordner angelegt. Öffnen Sie sie. In den Dateinamen der Fachlogik finden Sie die Begriffe Ihres Datenmodells wieder. Fehlt einer, oder taucht einer auf, den Sie nicht festgelegt haben, ist das eine Frage an den Agenten.
- **Die Daten.** Irgendwo liegt die Ablage der Daten, oft eine kleine Datenbank. Im Quelltext stehen dann Befehle in einer zweiten Sprache, die die Tabellen anlegen und füllen. Auch darin erkennen Sie Ihre Begriffe wieder: eine Tabelle je Ding aus dem Datenmodell.
- **Die Tests.** Zum Ergebnis gehören Tests der wesentlichen Funktionen. Ein Test ist ein kleines Programm, das eine Funktion aufruft und prüft, ob das Ergebnis stimmt: drei Pakete auslagern, danach müssen sieben da sein. Lesen Sie die Namen der Tests gegen die Anforderungen. Jede Anforderung sollte hinten ihren Test finden, so war die Kette gedacht.

Dann starten Sie das Programm. Dafür öffnen Sie ein zweites Terminal neben dem, in dem der Agent läuft, denn der Agent soll weiterleben, während Sie probieren. Lagern Sie etwas ein, lagern Sie es wieder aus, lassen Sie sich den Bestand zeigen. Fragen Sie den Agenten nach dem Befehl zum Starten, er hat das Programm gebaut und kennt ihn.

## Was der Kontext dabei kostet

Bauen ist für das [Kontextfenster](../Z-anhang/Z010-glossar.md#kontextfenster) teurer als Reden. Jede Datei, die der Agent schreibt, geht als Text durch seinen Kontext. Jedes Befehlsergebnis, jede Fehlermeldung, jeder Testlauf ebenso. Eine Implementierung, die aus zwanzig Dateien besteht, ist zwanzigmal Text hinein und Text heraus. Bezahlt werden die [Tokens](../Z-anhang/Z010-glossar.md#token) in beide Richtungen, direkt oder aus Ihrem Kontingent (Stand Oktober 2026).

Die zweite Rechnung ist die aus dem Kapitel [Kontext](../A-verstehen-und-loslegen/A020-kontext.md): Das Fenster ist begrenzt, und beim Bauen füllt es sich schnell. Irgendwann fasst der Agent zusammen, und Einzelheiten gehen verloren. Deshalb zwei Gewohnheiten, die Sie sich beim ersten Bauen aneignen sollten. Beobachten Sie die Anzeige des Kontexts, während der Agent arbeitet, um ein Gefühl dafür zu bekommen, bevor er zur Neige geht. Und sorgen Sie dafür, dass alles Ausgearbeitete auf der Platte liegt, nicht nur im Gespräch. Für die Dokumente der Kette gilt das schon. Für die Entscheidungen, die während des Bauens fallen, noch nicht.

## Die Prüfung bleibt bei Ihnen

Der Agent meldet: fertig, die Tests laufen durch. Was heißt das? Es heißt, dass das Programm die Prüfungen besteht, die der Agent selbst geschrieben hat. Derselbe Agent hat die Anforderungen gelesen, die Spezifikation geschrieben, den Quelltext geschrieben und die Tests dazu, alles in einem Kontext. Hat er eine Anforderung falsch verstanden, dann steckt das Missverständnis in der Spezifikation, im Quelltext und im Test gleichermaßen, und der Test ist grün.

Ob das Programm tut, was Sie wollten, wissen deshalb nur Sie. Nehmen Sie `anforderungen.md` und gehen Sie die Anforderungen Punkt für Punkt durch, am laufenden Programm. Was fehlt oder falsch ist, geht zurück ins Gespräch, und der Agent bessert nach. Das ist im naiven Ansatz die ganze Prüfung, und sie hat zwei Schwächen: Sie können nicht alles lesen, und Sie prüfen gegen Dokumente, die derselbe Agent geschrieben hat. Wie man unabhängig prüfen lässt, ist das Thema des Kapitels [Prüfen](../G-der-gesamtprozess/G020-pruefen.md). Für jetzt reicht: Grün heißt nicht richtig.

## Was jetzt klar sein sollte

- Bauen lassen ist der kürzeste Auftrag der Kette, weil die Arbeit in den Dokumenten steckt. Die Sprache müssen Sie nicht können.
- Lesen heißt, den Aufbau gegen die Dokumente zu halten: Fachlogik gegen das Datenmodell, Oberfläche gegen die Abläufe, Tests gegen die Anforderungen. Dann starten und probieren.
- Bauen füllt das Kontextfenster schneller als Reden und kostet Tokens in beide Richtungen. Beobachten Sie den Kontext, und halten Sie Ausgearbeitetes auf der Platte.
- Grüne Tests zeigen, dass das Programm die eigenen Prüfungen des Agenten besteht. Ob es das Richtige tut, prüfen Sie.

Weiter mit [Wo der Ansatz bricht](B040-wo-der-ansatz-bricht.md): Das Programm läuft, und dann kommt die erste Änderung.
