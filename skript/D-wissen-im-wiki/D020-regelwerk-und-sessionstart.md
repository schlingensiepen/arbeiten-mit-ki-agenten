# Regelwerk und Sessionstart

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `MasterPrompt.md`, `Styleguide.md`, `docs/Arbeitsweise.md`, `devstate_active.md`.

> **Der Plan steht in der Datei. Geht der Kontext verloren, ist der Plan noch da.**

Das Wissen über das Projekt liegt im Wiki. Woher aber weiß der Agent, wie er in diesem Projekt arbeiten soll? Was liest er beim Start, wo steht, wie weit die Arbeit ist, und wie läuft eine Sitzung vom ersten bis zum letzten Schritt? Dieses Kapitel beantwortet das mit drei Dateien, die drei verschiedene Aufgaben haben, und mit einem festen Ablauf, dem Sessionstart. Am Ende steht ein Rat, der die Arbeit mit einem Agenten dauerhaft verändert: Lassen Sie ihn sich erst ein Werkzeug bauen.

## Drei Dateien, drei Aufgaben

**Das Regelwerk.** Das [Regelwerk](../Z-anhang/Z010-glossar.md#regelwerk) sind die Dateien, die festlegen, wie ein Agent in einem Projekt arbeitet. Die eine Quelle aller Regeln ist `MasterPrompt.md`; umfangreichere Themen sind in Teildateien ausgelagert: `Wiki.md` für die Logik des Wikis, `Vorgehen.md` für Phasen und Freigaben, `Reviewmuster.md` für Prüfungen, `Outgoing.md` für den Versand, dazu Styleguides für Sprache und Form. Der mitgelieferte `Styleguide.md` setzt Deutsch als Projektsprache und einen sachlichen, bestimmten Ton. Das Regelwerk wird in das Projekt kopiert und lebt dort. Der Agent liest es aber nicht bei jedem Start, sondern nur auf Anweisung. Der Grund ist wieder das Fenster: Was beim Start im Kontext liegt, belegt Platz für die ganze Sitzung. Ein Regelwerk von vielen Seiten gehört nicht dorthin.

**Die Instruktionsdatei.** Was der Agent beim Start automatisch lädt, ist die [Instruktionsdatei](../Z-anhang/Z010-glossar.md#instruktionsdatei). Sie heißt je nach Agent anders, etwa `CLAUDE.md` oder `.cursorrules`; jeder Agent leitet seine eigene aus dem MasterPrompt ab, alle sind Sichten auf dieselbe Quelle. Sie ist der verpflichtende Minimal-Kontext vor der ersten Nachricht und bleibt klein, weil jedes Wort darin Kontext kostet. Sie enthält feste Abschnitte: wer das Projekt ist, die eisernen Regeln, darunter das Grundgesetz „das Wiki ist die Quelle der Wahrheit“, Verweise ins Regelwerk, die Arbeitsmodi und Git-Regeln, die Projektsprache, Besonderheiten des Projekts und eine Konfigurations-Übersicht. Diese Übersicht ist automatisch aus dem Wiki erzeugt und trägt einen Warnhinweis: Änderungen gehören in die Quellen, nicht hierher. Die Instruktionsdatei ändert sich selten. Ändert sich der MasterPrompt, zieht der Agent seine Datei nach; weicht die gespiegelte Konfiguration vom Wiki ab, überschreibt er nicht still, sondern fragt, was gilt.

**Der Arbeitsstand.** Wie weit die Arbeit ist, steht weder im Regelwerk noch in der Instruktionsdatei, sondern in `devstate_active.md`, dem [Arbeitsstand](../Z-anhang/Z010-glossar.md#arbeitsstand). Die Datei hat drei Abschnitte: wo das Projekt gerade steht, in drei bis fünf Sätzen mit der laufenden Marke, die nächsten Schritte und Blockaden oder Risiken. Der Agent pflegt sie ab dem ersten Tag. Für die Lagerverwaltung könnte dort stehen: Marke 1.0, die Anforderungen für Einlagern und Auslagern sind angenommen, der Report ist noch Entwurf; nächster Schritt ist die Funktionsbeschreibung des Auslagerns. Das ist der Plan aus dem Satz am Kapitelanfang. Wird der Kontext verdichtet oder beginnt morgen eine neue Sitzung, steht dort immer noch, wo man war: wir sind bei Schritt 5.

Der Arbeitsstand hat noch eine zweite Aufgabe. Er ist ein Schaufenster für jemanden, der von außen auf das Projekt schaut und nicht erst die Register durcharbeiten will. Deshalb wiederholt er, was in den Registern genauer steht. Diese Redundanz ist gewollt; sie ist der Preis dafür, dass man die Lage in einer Minute erfasst.

Die Festlegungen selbst, also was gilt und warum, stehen in keiner dieser drei Dateien, sondern im Wiki, in den Registern aus dem Kapitel [Register und Elemente](D040-register-und-elemente.md). Zusammengefasst: Regeln im Regelwerk, Einstieg in der Instruktionsdatei, Stand im Arbeitsstand, Festlegungen im Wiki.

## Der Sessionstart

Jede Sitzung beginnt gleich, mit dem [Sessionstart](../Z-anhang/Z010-glossar.md#sessionstart). Beim allerersten Mal kommen die Schritte des Einrichtens hinzu; die stehen im Kapitel [Ein Projekt aufsetzen](D030-ein-projekt-aufsetzen.md). Danach läuft der Start so ab:

1. **Orientieren.** Der Agent prüft, ob ein Git-Repository da ist und ob Änderungen uncommittet herumliegen; das meldet er, blockiert aber nicht. Er prüft seine Instruktionsdatei: vorhanden, vollständig, jünger als der MasterPrompt. Fehlende Standardordner legt er ohne Rückfrage an.
2. **Kontext laden.** Nicht alles wird gelesen. Vollständig liest er die Instruktionsdatei, die Landkarte der Fassaden, die Projektfakten mit Vorrang für die Stolpersteine, die Regeln für das Gespräch, offene Fragen, Fristen, die Werkzeugliste und Ihre offenen Punkte. Die übrigen Fassaden und die Styleguides merkt er sich nur und liest sie, wenn er sie braucht. Das Mission Statement liest er nicht, es ist für Menschen geschrieben. Und auch der geladene Kontext ersetzt das Nachschlagen nicht: Vor einer Behauptung schlägt er im Wiki nach.
3. **Abgleichen.** Der Agent sucht, was seit der letzten Sitzung liegen geblieben ist: Originale ohne Umwandlung, Dokumente ohne Wiki-Knoten, abgelaufene Fristen, fällig gewordene Einträge, Widersprüche zwischen Fassade und Knoten, Commits mit falschem Präfix. Alles wird nur vorgemerkt, nichts blockiert. Die Leitlinie lautet: lieber ein Hinweis mehr als einer zu wenig.
4. **Melden.** Die Befunde kommen in einer einzigen Nachricht mit drei strikt getrennten Blöcken: **Erledigt**, was der Agent getan und festgestellt hat; **Aktion**, was er als Nächstes tut, wenn Sie nicht widersprechen; **Frage**, was er wirklich von Ihnen braucht, höchstens ein bis zwei Punkte. Interne Nummern und Paragraphen des Regelwerks nennt er Ihnen gegenüber nicht.
5. **Bereit.** Zum Schluss schreibt er „Bereit für den ersten Auftrag.“ und wartet. Gab es nichts zu melden, verkürzt sich alles auf „Sessionstart abgeschlossen. Keine offenen Punkte.“

![Oben links zwei grüne Blöcke, Instruktionsdatei, automatisch geladen, und Wiki und Arbeitsstand, nach Bedarf gelesen. Pfeile führen in einen blauen Block Sessionstart mit den Schritten orientieren, Kontext laden, abgleichen, von dort in einen gelben Block Meldung mit Erledigt, Aktion, Frage und dem Text Bereit für den ersten Auftrag. Darunter eine zweite Reihe: grüner Block Auftrag vom Menschen, blauer Block Zug, blauer Block Commit, rechts der Text Sitzungsende, Abschluss-Commit. Ein oranger Pfeil führt vom Commit zurück zum Auftrag, beschriftet nächster Zug.](bilder/D020-sessionstart.svg)

**Ablauf einer Sitzung.** Der Sessionstart baut den Kontext aus den Dateien auf und endet mit der Meldung in drei Blöcken. Danach folgt Zug auf Zug, jeder mit einem Commit, bis zum Abschluss-Commit am Ende.

## Arbeiten in Zügen

Nach dem Start kommt Ihr Auftrag, und die Arbeit läuft in Zügen. Ein Zug ist eine thematisch abgeschlossene Einheit aus mehreren Arbeitsschritten: ein Dokument ins Wiki übernehmen, eine neue Version eines Ausgangsdokuments, eine Änderung im Wiki, die Installation eines Werkzeugs. Je Zug ein [Commit](../Z-anhang/Z010-glossar.md#commit), nicht mehr und nicht weniger; Züge werden nicht gebündelt, leere Commits gibt es nicht. Jede Commit-Nachricht beginnt mit einem Präfix aus einem festen Katalog, etwa `Wiki:` oder `Setup:`, in der Sprache, die Sie beim Einrichten festgelegt haben. Am Ende der Sitzung folgt ein Abschluss-Commit für alles, was noch nicht erfasst ist, damit der Arbeitsbaum sauber bleibt. Gepusht wird nur auf Ihre Anfrage.

Bei Commits, die Code ändern, lässt der Agent vorher die Prüfwerkzeuge des Projekts laufen und schreibt das Ergebnis in die Commit-Nachricht. Ein rotes Ergebnis blockiert den Commit nicht; die Zeile macht in der Historie sichtbar, welcher Commit ein Zwischenstand war und welcher ein grüner Meilenstein.

Der Grund für diese Kadenz ist derselbe wie beim Wiki. Vor jeder Pause stellt der Agent den Zustand her, in dem ein anderer Agent allein aus den Dateien weiterarbeiten könnte: offene Klärungen in Dateien, Fassaden nachgezogen, alles committet. Das Regelwerk nennt das Handoff. Wer so arbeitet, kann jederzeit unterbrochen werden, ohne dass etwas verloren geht. Warum Git dabei das Gedächtnis ist, stand im Kapitel [Git als Gedächtnis](../A-verstehen-und-loslegen/A060-git-als-gedaechtnis.md).

Im Betrieb fragt der Agent bei Unklarheit nach und führt nicht aus; mechanische Standardaufgaben wie Commits oder die Pflege des Index erledigt er ohne Rückfrage, meldet sie aber. Wer was entscheidet, ist das Thema des Teils [Mensch und Agent](../E-mensch-und-agent/README.md).

## Der Agent baut sich sein Werkzeug

> **Sagen Sie dem Agenten nicht: Mach das. Sagen Sie ihm: Schreib dir erstmal ein Tool.**

Im Kapitel [Was ein Agent ist](../A-verstehen-und-loslegen/A010-was-ein-agent-ist.md) haben Sie gesehen, warum Befehle eines Terminals so gut zu einem Agenten passen: Text hinein, Text heraus, und das Ergebnis landet unverändert im Kontext. Das Regelwerk macht daraus einen festen Platz. Im Ordner `tools/` liegen die Projekt-Skripte des Agenten: Konverter, Skripte für die Übernahme vieler Dokumente, Prüfwerkzeuge, Automatisierungen. Jedes Skript wird in `Tools.md` eingetragen, mit Zweck und Aufruf, damit die nächste Sitzung es findet. Der Code des Produkts gehört nicht hierher, sondern in seine eigenen Ordner; `tools/` trägt nur die Werkzeuge des Agenten.

Ein Beispiel aus der Lagerverwaltung: Sie wollen wissen, ob in den Testdaten jeder Artikel genau einen Lagerplatz hat. Der Agent könnte die Datei lesen und Zeile für Zeile prüfen. Dann liegt die ganze Datei im Kontext, und beim nächsten Mal liest er sie wieder. Lassen Sie ihn stattdessen ein kleines Skript schreiben, das die Prüfung übernimmt und nur die Abweichungen ausgibt. Das Skript läuft in Sekunden, immer gleich, kostet beim zweiten Aufruf keinen neuen Gedanken, und im Kontext landen drei Zeilen statt dreihundert. Der Agent benutzt sein Werkzeug danach selbst, in dieser Sitzung und in jeder weiteren.

In `Tools.md` stehen außerdem die Werkzeug-Wahlen des Projekts: Erweiterungen wie MCP-Server oder Skills und die Prüfwerkzeuge. Erweiterungen installiert der Agent nicht eigenmächtig. Braucht ein Vorhaben ein Werkzeug, schlägt er vor, was verfügbar ist, und immer auch eine Variante ohne Werkzeug. Sie wählen.

## Was jetzt klar sein sollte

- Das Regelwerk legt fest, wie gearbeitet wird, und wird nur auf Anweisung gelesen. Die Instruktionsdatei ist der kleine, automatisch geladene Einstieg. Der Arbeitsstand sagt, wo das Projekt steht. Die Festlegungen liegen im Wiki.
- Der Sessionstart baut den Kontext jedes Mal neu aus den Dateien auf: orientieren, laden, abgleichen, melden in drei Blöcken, bereit.
- Die Arbeit läuft in Zügen mit je einem Commit, mit Abschluss-Commit am Ende, damit jederzeit jemand anderes übernehmen könnte.
- Ein Werkzeug statt einer Handarbeit spart Kontext und bleibt dem Projekt erhalten.

Weiter mit [Ein Projekt aufsetzen](D030-ein-projekt-aufsetzen.md): wie aus einem leeren Ordner und einem Satz ein Projekt mit Regelwerk und Wiki wird.
