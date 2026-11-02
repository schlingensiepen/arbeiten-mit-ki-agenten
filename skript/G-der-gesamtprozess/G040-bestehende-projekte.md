# Bestehende Projekte

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Migration.md`, `docs/Upgrade.md`, `migration/MIGRATION.md`, `upgrade/UPGRADE.md`, `setup/init-migration.sh`, `setup/upgrade.sh`.

Das Kapitel [Ein Projekt aufsetzen](../D-wissen-im-wiki/D030-ein-projekt-aufsetzen.md) ging von einem leeren Ordner aus. Die meisten Projekte sind nicht leer. Entweder gibt es schon Code und Notizen, aber kein Regelwerk; oder das Projekt arbeitet schon mit der Vorlage, nur mit einem älteren Stand. Für beide Fälle hat die Vorlage einen Sonderweg: die [Migration](../Z-anhang/Z010-glossar.md#migration) bringt ein Projekt ohne Regelwerk nachträglich unter das Regelwerk, das [Upgrade](../Z-anhang/Z010-glossar.md#upgrade) hebt ein Projekt aus der Vorlage auf deren neuen Stand. Dieses Kapitel zeigt beide so weit, dass Sie wissen, was auf Sie zukommt und was Sie entscheiden. Die Einzelheiten stehen in der Anleitung, die der Agent selbst liest.

Welcher Weg gilt, erkennt der Agent am Projekt. Ein Projekt aus der Vorlage trägt einen Herkunfts-Vermerk in der Datei `wiki/Aktivierter-Prozess.md`; ein sehr frühes Projekt ohne Vermerk erkennt er daran, dass die Dateien des Regelwerks neben einem `wiki/` liegen. Das ist ein Upgrade. Ein Ordner, der sein Wissen in verstreuten Dateien sammelt, ist eine Migration. Der Agent sagt Ihnen, was er vorfindet; erkennt er den falschen Weg, verweist er auf den richtigen.

## Drei Grundsätze für beide Wege

Migration und Upgrade folgen denselben drei Grundsätzen. Wo die Anleitung einen Fall nicht nennt, entscheiden sie:

- **Nichts geht verloren.** Nichts wird überschrieben, nichts gelöscht ohne Ihren ausdrücklichen Wunsch. Darum steht am Anfang ein Sicherungs-[Commit](../Z-anhang/Z010-glossar.md#commit) des unveränderten Zustands, und jede vorgefundene Datei bleibt liegen. Umbenennen ist die einzige Änderung, die der Agent an ihr vornimmt.
- **Alles wird einsortiert.** Was der Agent vorfindet, überträgt er in die Struktur der Vorlage oder verlinkt es, und die Herkunft bleibt erkennbar. Nie wird etwas verworfen.
- **Im Zweifel fragt er Sie.** Gesammelt, in einem Block. Danach arbeitet er autonom und meldet sich nur bei echten Blockaden.

Dazu gilt: Keine Ausführung ohne Zustimmung. Jedes Kommando, das etwas verändert, nennt der Agent vorher und wartet auf Ihre Antwort. Ausgenommen sind die Commits, die nur sichern oder aufnehmen; die kündigt er in einem Satz an.

## Migration: ein Projekt ohne Regelwerk

Die Migration ist für ein Projekt gedacht, das sein Wissen in verstreuten Dateien sammelt: eine README, ein Changelog, Aufgabenlisten, Architektur-Notizen, vielleicht eine [Instruktionsdatei](../Z-anhang/Z010-glossar.md#instruktionsdatei) für den Agenten. Dieses Wissen überführt der Agent ins Wiki, ohne eine vorgefundene Datei zu verändern. Sie starten ihn im Projektordner mit einem Satz:

```text
Migriere das Projekt in diesem Verzeichnis nach der Anleitung unter https://github.com/schlingensiepen/referenzprozess-softwareentwicklung.
```

Der Agent liest die Anleitung von dort. Das Regelwerk zieht er erst heran, wenn eine Phase ihn dorthin schickt; der Kontext bleibt geschont. Dann läuft die Migration in Phasen, jede endet mit einem Commit.

**Sicherung und Aufnahme.** Zuerst der Sicherungs-Commit. Fehlt ein [Git](../Z-anhang/Z010-glossar.md#git)-Repo, bietet der Agent an, eines anzulegen, und wartet. Dann bindet er die Vorlage als `_template/` ein, wie beim Projektstart, und kopiert die Projektdateien, per Skript oder von Hand:

```sh
sh _template/setup/init-migration.sh
```

Das Skript überschreibt nie eine vorgefundene Datei. Trägt eine Datei denselben Namen wie eine Datei der Vorlage, lässt es sie aus und nennt sie. Zum Schluss ein Aufnahme-Commit. Die Historie trennt so sauber „vorher“ von „Vorlage da“.

**Der Fragen-Block.** Alles, was der Agent von Ihnen braucht, fragt er in einem Block, je Punkt mit seinem Vorschlag zuerst. Er bestätigt mit Ihnen, welche Dateien die bisherigen Wissensträger sind und welche offene Arbeiten enthalten. Er schlägt zwei Prüfer verschiedener Modelle für die Absicherung vor und fragt nach dem Ersatzweg, falls es nur ein Modell gibt, wie im Kapitel [Prüfen](G020-pruefen.md). Er fragt nach der Rolle des Projekts und nach den Ordnern, die bleiben sollen. Und er stellt die Kollisionsfrage: Für jede vorgefundene Datei, deren Name mit einer Datei der Vorlage kollidiert, etwa eine eigene `TODO.md` oder eine Instruktionsdatei, gibt es drei Möglichkeiten: umbenennen und nur verlinken, komplett integrieren, oder integrieren und die alte Fassung behalten. Der umbenannte Name endet auf `-vorgefunden`. Gelöscht wird nichts, bis Sie es ausdrücklich sagen.

**Die Transformation.** Jetzt arbeitet der Agent autonom. Jede Art von Wissen in Ihren Dateien hat genau ein Ziel im Wiki. Ein Ausschnitt der Zuordnung:

| Was bisher in Dateien stand | Wohin es kommt |
|---|---|
| Anforderungen, Features, Soll-Verhalten | Register Anforderungen |
| Bekannte Fehler, offene Bugs | Register Fehlermeldungen |
| Beschreibungen, was die Software tut | Register Funktionsbeschreibungen |
| Getroffene Festlegungen, Beschlüsse | Register Entscheidungen |
| Architektur, Soll und dokumentierter Ist-Stand | Architektur-Fassade, der Ist-Stand als eigener Abschnitt |
| Testfälle | Register Testfälle |
| Fachbegriffe | Glossar, als Vorschläge zur Freigabe |
| Changelog, Release-Notizen | Chronologie; das Original bleibt liegen und wird verlinkt |
| Aufgabenlisten, Roadmaps | je Punkt ein Ziel; die Datei wird aus der neuen `TODO.md` verlinkt |
| Was nirgends passt oder nicht sicher rekonstruierbar ist | die Auffang-Datei `wiki/Migrations-Grundlagen.md` |

Jeder übertragene Eintrag nennt seine Herkunfts-Datei. Übernommene Elemente tragen keine Marke und kein Datum; sie sind Bestand und gelten ab ihrer Annahme. Erfunden wird nichts: keine rekonstruierten Daten, keine Zahlen, die nirgends stehen. Im Zweifel wählt der Agent den vorsichtigen Status und legt den Fall in die Auffang-Datei. Am Ende legt er eine neue `TODO.md` an, die jede vorgefundene Datei mit offenen Arbeiten verlinkt.

**Die Absicherung.** Zwei Prüfer prüfen als frische Agenten, unabhängig voneinander: Ist jede Wissensdatei vollständig übertragen? Verfälscht ein Eintrag seine Quelle? Liegt alles am richtigen Ort? Läuft der Lint ohne Fehler? Jeder schreibt einen Bericht mit Ampel. Sind beide grün, geht es weiter; sonst wird nachgearbeitet und erneut geprüft, höchstens drei Runden. Haben Sie sich selbst als Prüfer gewählt, prüfen Sie danach. Zum Schluss legt der Agent Ihnen die unsicheren Stellen vor, und Sie nehmen die Rekonstruktion als Ganzes an; das wird als [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) gebucht.

**Die Restfragen.** Erst jetzt kommen die Fragen des Projektstarts, die noch offen sind: die Freigabe der gesammelten Glossar-Vorschläge, die Sprache der Commits, ein Repo oder zwei wie im vorigen Kapitel, die Instruktionsdatei des Agenten. Danach gilt der normale Betrieb.

Was danach anders ist als bei einem neuen Projekt: Die erste [Marke](../Z-anhang/Z010-glossar.md#marke) heißt nicht „1.0“, sondern `Uebernahme-` mit dem Datum der Aufnahme. Sie bleibt offen, bis Sie ihre Freigabedokumente abgeleitet haben und die Marke regulär abschließen; in der Migration selbst entsteht kein Freigabedokument. Ihre alten Dateien liegen unverändert da, teils mit dem Zusatz `-vorgefunden`, und sind verlinkt.

### Beispiel: Die frühe Lagerverwaltung

In Teil B ist die Lagerverwaltung nach dem naiven Ansatz entstanden: ein Ordner mit einer README, einer Datei mit Anforderungen, einer mit der Architektur, einer Spezifikation, einem Testkonzept, dem Code und einer Aufgabenliste. Kein Wiki, kein Register, keine Marke. So wird sie migriert.

Der Agent sichert den Ordner mit einem Commit und bindet die Vorlage ein. Im Fragen-Block bestätigen Sie die sechs Dateien als Wissensträger; die Aufgabenliste ist die mit offenen Arbeiten. Die eigene `TODO.md` kollidiert mit der der Vorlage; Sie wählen, sie zu integrieren und die alte Fassung zu behalten. Dann arbeitet der Agent: Jede Anforderung aus der Anforderungsdatei wird ein Element im Register Anforderungen, mit der Datei als Herkunft. Die Architekturdatei wird zur Architektur-Fassade; was den gebauten Ist-Stand beschreibt, kommt in einen eigenen Abschnitt. Die Spezifikation beschreibt überwiegend, was die Software aus Sicht des Lageristen tut, also wandert sie in die Funktionsbeschreibungen; nur die Teile, die eine Bauanleitung sind, werden Spezifikation. Die Testfälle aus dem Testkonzept werden Elemente im Register Testfälle. Aus der README holt er die Festlegungen, etwa die Wahl der Programmiersprache, ins Register Entscheidungen. Die Punkte der Aufgabenliste verteilt er: Geplantes wird Anforderung, Unverbindliches wird Idee. Die alte Liste bleibt als `TODO-vorgefunden.md` liegen, die neue `TODO.md` verlinkt sie.

Zwei Prüfer lesen gegen, einer findet eine Anforderung, die beim Übertragen verkürzt wurde. Nach der Korrektur sind beide grün. Sie nehmen die Rekonstruktion an. Die Lagerverwaltung hat jetzt ein Wiki, die Marke `Uebernahme-` mit dem Datum, und als erste Aufgabe danach: die Freigabedokumente dieser Marke bilden und durch die Prüfkette führen, wie im Kapitel [Softwareentwicklung als Prozess](G010-softwareentwicklung-als-prozess.md).

## Upgrade: ein Projekt aus der Vorlage

Die Vorlage ändert sich. Sie trägt eine Versionsnummer, zum Zeitpunkt dieses Skripts 2.0 nach den früheren Ständen 1.0 und 1.1 (Stand Oktober 2026). Welchen Stand Ihr Projekt hat, steht im Herkunfts-Vermerk. Das Upgrade hebt das Projekt auf den aktuellen Stand derselben Vorlage, aus der es stammt, und es behält dabei seinen Prozess. Sie starten den Agenten im Projektordner mit einem Satz:

```text
Hebe das Projekt in diesem Verzeichnis auf den aktuellen Stand nach der Anleitung unter https://github.com/schlingensiepen/referenzprozess-softwareentwicklung.
```

Der Ablauf hat eine Frage und acht Schritte. Die Frage kommt zuerst: Der Agent liest, welchen Stand und welche Einbindung das Projekt hat, legt Ihnen eine Übersicht vor und schlägt den Weg vor. Mit Ihrer Antwort führt er die Schritte aus; Sie stoßen nur an.

1. **Sicherung.** Ein Commit des unveränderten Zustands, angekündigt.
2. **Vorlage tauschen.** `_template/` bekommt den neuen Stand: bei einer verknüpften Vorlage wird das Submodul weitergesetzt, bei einer eingefrorenen Kopie wird die Kopie ersetzt. Die alte bleibt in der Git-Geschichte. Danach ein eigener Commit.
3. **Mechanik.** Ein Skript erledigt, was keine Inhalte berührt:

   ```sh
   sh _template/setup/upgrade.sh
   ```

   Mit `--nur-pruefen` zeigt es vorher, was es täte. Es benennt Dateien um, die im neuen Stand anders heißen, legt Dateien an, die im Projekt fehlen, stellt Formalien in den Köpfen der Knoten um und schreibt die Versionsfolge in den Herkunfts-Vermerk. Eine bestehende Datei überschreibt es nie. Was es nicht mechanisch erledigen kann, etwa Links auf umbenannte Dateien, listet es für den Agenten auf, der es mit Blick auf den Zusammenhang nachzieht. Ein zweiter Lauf ändert nichts mehr.
4. **Pflicht-Fassaden und laufende Marke.** Register, die in jedem Projekt Pflicht sind, werden aktiv; fehlt eine Marke, die gerade läuft, legt der Agent die von Ihnen genannte an.
5. **Delta-Nachzug.** Für jede Datei, die es im Projekt und im neuen Stand gibt, etwa das Regelwerk im Projektordner oder die Köpfe der Fassaden, vergleicht der Agent beide und legt Ihnen die Unterschiede als Vorschläge vor. Überschrieben wird nichts.
6. **Versionssprung.** Was der Sprung von einer bestimmten alten auf die neue Version zusätzlich verlangt, steht in einer eigenen Datei der Vorlage.
7. **Herkunft.** Der Herkunfts-Vermerk trägt danach die neue Version mit dem Tag des Upgrades und darunter die alte mit ihrem Ende. Ein Projekt sammelt so seine Versionsfolge. Der Tag des Upgrades ist zugleich der Stichtag für den Lint: Neue Pflichtfelder gelten als Fehler nur für Elemente ab diesem Tag; für den Bestand sind sie Hinweise.
8. **Absicherung.** Der Lint ohne Fehler, dann zwei Prüfer verschiedener Modelle als frische Agenten, mit Ampel und höchstens drei Runden wie bei der Migration, danach Sie, wenn Sie Prüfer sind. Zum Schluss der Abschluss-Commit.

Danach gilt für die laufende Marke die normale Prüfkette. Die Anleitung bleibt in der Vorlage und wird nicht ins Projekt kopiert. Davon getrennt ist das Hinzufügen oder Wechseln eines Referenzprozesses; es läuft als eigener Vorgang, und wenn dabei bestehende Einträge umgebaut werden, folgt dieselbe Absicherung.

## Was jetzt klar sein sollte

- Migration und Upgrade sind die Wege für Projekte, die schon da sind. Die Migration bringt Wissen aus verstreuten Dateien ins Wiki; das Upgrade hebt ein Projekt aus der Vorlage auf deren neuen Stand. Der Agent erkennt am Herkunfts-Vermerk, welcher Weg gilt.
- Beide folgen denselben Grundsätzen: Nichts geht verloren, alles wird einsortiert, im Zweifel fragt der Agent, gesammelt in einem Block. Kein Kommando ohne Ihre Zustimmung.
- Die Migration endet mit einer Marke `Uebernahme-` und dem Datum; übernommene Elemente sind Bestand ohne Marke, alte Dateien bleiben liegen. Das Upgrade endet mit einer neuen Zeile im Herkunfts-Vermerk.
- Beide schließen mit derselben Absicherung: Lint, zwei Prüfer mit Ampel, dann Sie.

Weiter mit [Subagenten](../H-mehrere-agenten/H010-subagenten.md): Teil H nimmt weitere Agenten hinzu, zuerst den Helfer mit leerem Kontext für einen abgegrenzten Auftrag.
