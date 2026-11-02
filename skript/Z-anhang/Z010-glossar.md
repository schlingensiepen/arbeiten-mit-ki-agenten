# Glossar

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Begriffe.md`; [peeragent](https://github.com/schlingensiepen/peeragent) `v0.2.0`, `docs/glossary.md`.

Die Wörter dieses Skripts in je ein bis drei Sätzen, alphabetisch. Jedes Kapitel verlinkt einen Fachbegriff beim ersten Auftreten hierher. Wer von hier kommt, findet die Definition; der Zusammenhang steht im Kapitel, das den Begriff einführt. Englische Fachwörter, die im Deutschen üblich sind, bleiben stehen und werden erklärt. Wo das Regelwerk ein anderes Wort benutzt als das Skript, steht es dabei.

## Ablösung

Ersatz eines Elements durch ein neues mit neuer Nummer. Das alte bleibt sichtbar stehen.

## Accept Edits

Berechtigungsstufe, bei der der Agent Dateien ohne Rückfrage ändern darf, für Befehle aber weiter fragt.

## Agent

Ein Sprachmodell mit einem Harness, der Tools aufrufen kann. Der Agent arbeitet im Projektordner, liest und schreibt Dateien und führt Befehle aus.

## Ampel

Gesamturteil eines Prüfers über ein Ergebnis: grün, gelb oder rot.

## Anforderung

Was ein Programm können muss oder können kann, als Satz festgehalten und nummeriert. „Schnell“ ist keine Anforderung, solange nicht dabeisteht, woran man es misst. Im Regelwerk ist eine Anforderung ein Element im Register der Anforderungen.

## Antwort-Raster

Feste Form der strukturierten Meldungen des Agenten: Erledigt, was getan ist; Aktion, was er als Nächstes tut, wenn man nicht widerspricht; Frage, was er vom Menschen braucht.

## Arbeitsmodus

Betriebsart für große Mengen, nur mit Zustimmung des Anwenders: Der Agent fragt bei Unklarheit nicht nach, sammelt die Fragen in der Datei `Offene Fragen.md`, überspringt den Teilschritt und arbeitet weiter.

## Arbeitsstand

Die Datei `devstate_active.md`: wo das Projekt gerade steht. Sie dient der nächsten Sitzung und ist zugleich ein Schaufenster für jemanden, der von außen draufschaut.

## Attribut

Eine Eigenschaft, die ins Modell aufgenommen wird, etwa die Artikelnummer eines Artikels. Welche Eigenschaften Attribute werden und wie genau sie sind, entscheidet der Anwendungsfall: so genau wie nötig, nicht genauer.

## Aufpasser-Modell

Zweites Modell, das nach dem, was man aus der Branche hört, beim Anbieter das erste überwacht.

## Auftragsdatei

Datei im Arbeitsverzeichnis eines zweiten Agenten, in der alles steht, was er für seine Arbeit braucht. Der Prompt, den er beim Start bekommt, zeigt nur auf diese Datei.

## Auswahlmenü

Vom Agenten angebotene feste Antworten auf eine Frage, die mit einem Tastendruck oder einem Wort gewählt werden; eine eigene Antwort ist immer möglich.

## Backend

Der Teil eines Systems, der im Hintergrund auf einem zentralen Rechner läuft und die Daten hält, im Gegensatz zu den Oberflächen wie App oder Kommandozeile.

## Bearbeiter-Kürzel

Drei Buchstaben, die zeigen, wer eine Datei bearbeitet hat. Der Agent hat ein eigenes Kürzel.

## Berechtigungsstufe

Einstellung, wie weit ein Agent ohne Rückfrage handeln darf, von der Einzelfreigabe jedes Schritts bis Skip Permissions.

## Briefing-Modus

Abarbeiten mehrerer Klärpunkte einzeln: je Punkt ein kurzes Briefing, dann Diskussion, weiter erst auf ausdrücklichen Zuruf. Zuerst kommt die Frage, deren Antwort am meisten anderes mitentscheidet.

## Chatbot

Ein Sprachmodell mit einem Eingabefeld: Es antwortet, handelt aber nicht selbst.

## Cheat-Sheet

Kurze Liste der wichtigsten Befehle zum Nachschlagen.

## clawbook

Fertig eingerichteter Arbeitsrechner für die Arbeit mit KI-Agenten als Container-Image, das sich unter Windows ohne Administrator-Rechte starten lässt. Eine Möglichkeit neben dem selbst installierten Agenten und dem der Firma.

## Commit

Ein gesicherter Zwischenstand in Git mit einer Beschreibung, was sich geändert hat. Zu jedem Commit lässt sich zurückkehren.

## Compact

Das Zusammenfassen des bisherigen Gesprächs, wenn das Kontextfenster voll wird. Es schafft Platz, Einzelheiten gehen dabei verloren. Es läuft automatisch oder auf Befehl; weil das Modell zum Zusammenfassen selbst Platz braucht, bleibt dafür ein Puffer im Fenster reserviert.

## Container

Abgeschlossene Umgebung auf einem Rechner, die ihre eigene Software mitbringt und vom Rest weitgehend getrennt ist.

## Datenmodell

Der Teil einer Software, der den Zustand der Welt beschreibt, im Beispiel der Lagerverwaltung den Bestand des Lagers: welche Dinge es gibt, welche Attribute sie haben und wie sie zusammenhängen.

## Dokumentenkette

Der naive Ansatz: je Schritt der Softwareentwicklung ein Dokument, jedes baut auf dem vorigen auf.

## Einfrieren

Der Inhalt eines Elements oder Dokuments wird ab einem Zeitpunkt nicht mehr geändert. Jede Änderung ergibt etwas Neues.

## Element

Nummerierter Eintrag in einem Register, etwa eine Anforderung oder eine Entscheidung. Es wird nicht überschrieben, sondern durch ein neues Element abgelöst, und geht in Freigabedokumente ein.

## Entscheidung

Festgelegte Projekt-Wahrheit mit Nummer, Wahl und Begründung. Sie kommt nur mit dem OK des Anwenders ins Register, ist ab dann eingefroren und wird nur durch eine neue Entscheidung abgelöst.

## Ersatzweg

Weg einer Prüfung, die ein zweites Modell verlangt, wenn kein Werkzeug ein zweites Modell bereitstellt: dasselbe Modell prüft in frischem Kontext, mit sichtbarer Einschränkung in der Freigabe, oder ein Mensch prüft. Der Anwender wählt ihn beim Aufsetzen des Projekts.

## Fassade

Übersichtsdatei im Wiki, am Stück lesbar, je Thema genau eine.

## Freigabe

Die Erklärung, dass ein Freigabedokument für einen bestimmten Zweck verlässlich ist, gebucht als Entscheidung in der Form „Stand x von ⟨Artefakt⟩, freigegeben für Zweck Z“. Sie wird nie zurückgenommen, eine Änderung ergibt ein neues Dokument mit neuer Freigabe.

## Freigabedokument

Allgemeinverständlicher Name für einen Stand: Das Dokument sammelt die Elemente einer Marke und friert sie ein, damit eine Freigabe etwas Festes hat, worauf sie sich bezieht.

## Getting Things Done

Methode, Aufgaben aus dem Kopf in ein verlässliches System zu holen und zu ordnen. Sie ist die Grundlage des Beispiels DONE.

## Gewichte

Die Zahlen in einem Modell, die beim Training angepasst werden. Sie sind das, was das Modell gelernt hat.

## Git

Programm, das die Geschichte eines Projekts aufzeichnet: Jede Änderung bleibt nachvollziehbar und lässt sich zurücknehmen.

## GitHub

Dienst im Netz, auf dem Git-Repos liegen, gesichert und für andere erreichbar.

## Harness

Das Programm um das Sprachmodell herum: Es legt dem Modell den Kontext vor, führt dessen Tool-Aufrufe aus und steckt die Ergebnisse in den nächsten Prompt. Das Wort heißt wörtlich Zaumzeug: Der Harness führt das Modell, ohne selbst klug zu sein.

## Inbox

Englisch für Postfach. Im Beispiel DONE heißt daneben die Ablage für Aufgaben ohne Tag Inbox, nach der Methode Getting Things Done.

## Init

Das einmalige Einrichten eines neuen Projekts aus dem Referenzprozess, in dem der Agent die Festlegungen abfragt, die er nicht ableiten kann.

## Instruktionsdatei

Die agent-spezifische Datei, die der Agent beim Start automatisch lädt, etwa `CLAUDE.md`. Weil jedes Wort darin Kontext kostet, bleibt sie klein.

## Kardinalität

Die Anzahl auf einer Seite einer Beziehung zwischen zwei Dingen im Modell: eins oder viele. Ob ein Artikel in einem Fach liegt oder in mehreren, ist eine Frage der Kardinalität, und die Antwort gibt der Anwendungsfall.

## Kettenprüfung

Siehe Prüfkette.

## Klärpunkt

Offene Frage, die der Agent nicht selbst entscheiden darf und dem Menschen zur Entscheidung vorlegt, mit Sachlage und Vorschlägen.

## Komponente

Eigenes Projekt mit eigenem Repo, in das ein größeres System geschnitten ist; sie liefert an den Koordinator.

## Kontext

Alles, was dem Sprachmodell bei einer Antwort vorliegt: Systemprompt, automatisch geladene Dateien, das bisherige Gespräch und Tool-Ergebnisse.

## Kontextfenster

Die begrenzte Menge an Text, die dem Sprachmodell auf einmal vorgelegt werden kann. Es wird je Runde vollständig neu vorgelegt. Das Skript sagt oft kurz Fenster.

## Konzept-Sammlung

Mitgelieferte Sammlungen erprobter Arbeitsweisen; der Agent schlägt beim Einrichten vor, welche zum Projekt passen.

## Koordinator

Das Projekt, das ein System in Komponenten zerlegt und deren Lieferungen integriert.

## Lint

Prüfung durch ein Programm ohne Modell. Sie findet Formfehler wie tote Links und fehlende Felder, ob der Inhalt stimmt, beurteilt sie nicht.

## LLM

Abkürzung für Large Language Model, deutsch Sprachmodell: ein trainiertes Modell, das zu einem Text die wahrscheinliche Fortsetzung erzeugt. Text hinein, Text heraus, mehr tut es nicht.

## Loss-Function

Funktion, die beim Trainieren eines Modells misst, wie groß der Fehler ist. Lernen heißt, ihr Minimum zu suchen.

## MADR

Ein festes Format, um Entscheidungen über den Aufbau einer Software aufzuschreiben. Beim Einrichten optional.

## Markdown

Textformat mit wenigen Auszeichnungen, etwa `#` für eine Überschrift und `-` für einen Listenpunkt. Menschen können es lesen, Modelle besonders gut; die Dateien des Wikis und dieses Skript sind Markdown.

## Marke

Ein benanntes Ergebnis, das nach außen geht und freigegeben wird, bei Software ein Release wie „1.0“ oder „1.1“. Eine Marke ist kein Datum und kein Meilenstein: Eine Frist kann zu ihr gehören, ihr Kern ist das Ergebnis. Jedes Element trägt seine Marke, genau eine Marke läuft, und eine abgeschlossene Marke ist eingefroren. Im Regelwerk heißt sie auch Zielmarke.

## MCP-Server

Programm, das einem Agenten nach einem festen Standard, dem Model Context Protocol, zusätzliche Tools zur Verfügung stellt. Der Unterschied zum Skill: Der MCP-Server sagt „ruf das auf“, der Skill sagt „hier steht, wie es geht“.

## Metamodell

Die Festlegung darüber, welche Arten von Dingen es im Modell gibt und welche Attribute und Beziehungen jede Art hat: das Modell des Modells. Es entsteht im Gespräch über die Anforderungen; die Daten kommen später, wenn das Programm läuft.

## Migration

Sonderweg, der ein bestehendes Projekt ohne Regelwerk nachträglich unter das Regelwerk bringt.

## Mission Statement

Kurze Beschreibung, was ein Projekt ist und für wen.

## Modell

Der Ausschnitt der Realität, den eine Software abbildet, so genau, wie der Anwendungsfall es braucht, und nicht genauer. Das Modell steht für die Realität, es ist nicht die Realität. Daneben sagt das Skript kurz Modell, wenn es das Sprachmodell meint.

## Nachricht

Datei, mit der ein Repo einem anderen etwas mitteilt, etwa eine Lieferung oder einen Änderungswunsch. Sie liegt nur beim Absender; der Empfänger bucht daraus in seine eigenen Register. Nicht gemeint sind eine Commit-Nachricht und ein Versand an Menschen. Was ein Agent einem anderen ins Postfach legt, heißt im Skript ebenfalls Nachricht; siehe Postfach.

## Nachweis

Eintrag in einem Register, der nie abgelöst, sondern nur mit Vermerken ergänzt wird: der Bericht eines Prüfers, ein Rechercheergebnis, ein eingegangenes Dokument. Gegenstück zum Element.

## peeragent

Werkzeug, das einen zweiten Agenten als eigenen Prozess in einer tmux-Sitzung startet.

## Phase

Wort des Regelwerks für einen Schritt des Gesamtprozesses, etwa Anforderungen sammeln oder Testen. Phasen ordnen Freigaben, nicht Arbeit.

## Planmodus

Betriebsart, in der der Agent erst einen Plan vorlegt, statt zu handeln. Technisch ist das ein weiteres Stück Prompt.

## Postfach

Der Eingang, in dem die Nachrichten für einen Agenten liegen, bis er hineinsieht; englisch Inbox. Beim einfachen Weg ein Verzeichnis, bei simple-a2a ein Postfach je Agent und Team.

## Produkt

Das, was eine Marke hervorbringt und nach außen geht, bei Software der Code mit seinen Tests. Es wird nicht als Dokument eingefroren, sondern in Git mit einem Tag markiert. Liegt es in einem eigenen Repo, heißt dieses Produkt-Repo, im Gegensatz zur Werkstatt.

## Prompt

Der Text, der dem Sprachmodell vorgelegt wird; im engeren Sinn die Eingabe des Menschen.

## Prozess

Die Folge der Phasen, die ein Projekt von der ersten Anforderung bis zur Auslieferung durchläuft, jede als Tätigkeit benannt und jede mit einem Freigabedokument als Ergebnis. Die Phasen sind ein Angebot und eine Checkliste, kein Zwang.

## Prüfer

Wer ein Ergebnis beurteilt, ohne daran mitgeschrieben zu haben: ein Subagent in frischem Kontext, ein zweiter Agent oder ein Mensch. Sein Ergebnis ist ein Bericht mit Befunden und einer Ampel.

## Prüfkette

Die Folge der Freigabedokumente einer Marke, in der jedes vor seiner Freigabe gegen seine freigegebenen Vorgänger geprüft wird: auf Widerspruch, Abdeckung und Unbegründetes. Das Regelwerk nennt sie Kette, die einzelne Prüfung Kettenprüfung. Nicht gemeint sind die Runden aus Prüfen, Einarbeiten und Re-Check.

## PWA

Programm, das im Browser läuft und sich wie eine App auf dem Telefon installieren lässt.

## Realm

Bei simple-a2a der abgegrenzte Bereich, in dem Teams und Agenten zusammenarbeiten.

## Reasoning

Fähigkeit eines Sprachmodells, vor der Antwort Zwischenschritte zu schreiben und so eine Aufgabe in Stufen zu lösen. Für den Agenten zählt, dass man das Modell damit nach dem nächsten Schritt fragen kann statt nach der Antwort.

## Re-Check

Erneute Prüfung, nachdem die Befunde einer Prüfung eingearbeitet sind.

## Referenzprozess

Vorlage für Softwareprojekte mit vorbereitetem Wiki, Regelwerk und Anleitungen für neues Projekt, Migration und Upgrade. Das Regelwerk unterscheidet genauer zwischen Starter und Prozess, im Skript steht das Wort für beides.

## Regelwerk

Die Dateien, die festlegen, wie ein Agent in einem Projekt arbeitet, mit dem MasterPrompt als Quelle aller Regeln.

## Register

Übersichtsdatei im Wiki mit nummerierten Einträgen, etwa Entscheidungen oder Anforderungen.

## Repo

Kurz für Repository: ein Projektordner unter der Aufsicht von Git mit seiner ganzen Geschichte.

## Review

Prüfdurchgang mit frischem Kontext, der einen Bericht und ein Urteil ergibt. Wer geprüft hat, hat nicht mitgeschrieben.

## Schleuse

Der geregelte Übergang von der Werkstatt ins Produkt: Kleinteilige Dokumente werden zu in sich vollständigen, und was nicht nach außen gehört, bleibt zurück.

## selbsttragend

Eigenschaft eines Dokuments, das am Stück an einen Empfänger ohne Zugang zum Wiki weitergegeben wird: keine Wikilinks, keine Register-Nummern, Begründungen ausgeschrieben. Gegenstück ist ein Dokument, das nur mit dem Wiki lesbar ist, weil es verlinkt statt wiederholt.

## Sessionstart

Der feste Ablauf zu Beginn jeder Sitzung: Der Agent orientiert sich, lädt den nötigen Kontext, gleicht Stände ab und meldet sich bereit.

## Shell

Programm, das Befehle in einem Terminal entgegennimmt und ausführt.

## simple-a2a

Kleines Protokoll, mit dem Agenten einander adressierte Nachrichten schicken. Der gleichnamige Dienst ist das Postamt dazu: Er befördert und bewahrt die Nachrichten und prüft, von wem sie kommen.

## Sitzung

Eine zusammenhängende Arbeit mit einem Agenten, von seinem Start bis zum Ende, mit einem eigenen Kontext.

## Skill

Anleitung für eine bestimmte Art von Aufgabe, die der Agent bei Bedarf in den Kontext lädt. Technisch ein weiteres Stück Prompt. Wer keine Mail verschickt, liest den Mail-Skill nicht; so bleibt das Fenster frei.

## Skip Permissions

Berechtigungsstufe, bei der der Agent ohne jede Rückfrage handelt. Nur auf einem wegwerfbaren Rechner ohne wertvolle Zugänge oder Daten und mit per Git gesicherter Arbeit.

## Sonderweg

Weg neben dem Projektstart aus der Vorlage, für Projekte, die schon da sind: die Migration für ein Projekt ohne Regelwerk, das Upgrade für ein Projekt mit einem älteren Stand der Vorlage.

## Spezifikation

Eine Bauanleitung, so genau, dass jemand danach programmieren kann, der das Grundproblem nicht kennt.

## Sprachmodell

Siehe LLM.

## Stand

Wort des Regelwerks für das Freigabedokument: ein Dokument, das zu einer Marke aus eingefrorenen Elementen gebildet wird und eine Freigabe trägt. Jede Änderung ergibt einen neuen Stand mit neuer Versionsnummer, der alte bleibt liegen. Nicht gemeint ist die Datumszeile einer lebenden Datei, im Regelwerk Bearbeitungsstand.

## Standardaufgabe

Mechanisch festgelegter Vorgang, etwa ein Commit, den der Agent ohne Rückfrage ausführt, weil die Regeln vollständig feststehen.

## Standard-Modus

Grundeinstellung des Agenten: Bei Unklarheit fragt er nach und führt nicht aus. Das gilt besonders für inhaltliche Entscheidungen und alles mit Außenwirkung.

## Startprompt

Der erste Prompt, mit dem ein Agent ein Vorhaben beginnt. Dazu zählt auch die Übergabe, die ein Koordinator für den Agenten einer neuen Komponente erzeugt.

## Subagent

Hilfs-Agent, den ein Agent mit eigenem, frischem Kontext für einen abgegrenzten Auftrag startet; zurück kommt nur sein Ergebnis. Im Regelwerk auch Unteragent.

## Submodul

Ein Repo, das als Unterordner in einem anderen Repo liegt und dort auf einen festen Commit zeigt. So liegt die Vorlage im Projekt oder das Produkt-Repo in der Werkstatt.

## Systemprompt

Der Teil des Prompts, den der Harness vorgibt: Er legt fest, wie sich das Modell verhält und dass es statt einer Antwort Tool-Aufrufe zurückgeben kann.

## Tag

Markierung in Git, die einen bestimmten Commit mit einem Namen versieht. Das Produkt einer Marke wird mit einem Tag markiert; ein Tag wird nie verschoben. Im Beispiel DONE heißt daneben ein Schlagwort an einer Aufgabe Tag.

## Team

Bei simple-a2a eine Gruppe von Agenten innerhalb eines Realms, die einander Nachrichten schicken können.

## Terminal

Fenster, in dem man Befehle tippt. Die Shell läuft darin und führt sie aus.

## tmux

Programm, das Terminal-Sitzungen vom Fenster löst, sodass ein Agent eine getrennte Verbindung überlebt.

## tmux-helper

Windows-Programm, das die tmux-Sitzungen entfernter Rechner auflistet und als Tabs im Windows Terminal öffnet.

## Token

Die Einheit, in der ein Sprachmodell Text zerlegt, etwa ein Wort oder ein Wortteil; lange zusammengesetzte Wörter werden in mehrere Tokens zerlegt. Kontextfenster und Kosten werden in Tokens gemessen.

## Tool

Fähigkeit, die der Harness dem Modell anbietet, etwa eine Datei lesen, einen Befehl ausführen oder im Web recherchieren. Ein Tool ist gewöhnliche Software: Text und Parameter hinein, Text heraus.

## Tool-Aufruf

Markierung im Text des Modells, die ein Tool anfordert. Das Modell führt nichts aus, der Harness tut es und gibt das Ergebnis zurück.

## Unteragent

Siehe Subagent.

## Upgrade

Sonderweg, der ein Projekt auf einen neuen Stand der Vorlage hebt.

## Vertrauensabfrage

Frage des Agenten beim ersten Start in einem Ordner, ob er diesem Ordner trauen soll.

## Verwerfen

Ein Element wird mit Begründung aufgegeben, ohne Nachfolger. Es bleibt sichtbar stehen.

## Verzicht

Bewusstes Auslassen einer Phase samt ihrem Freigabedokument für eine Marke, als Entscheidung gebucht. Für diese Marke entfallen damit das Dokument und seine Prüfpflichten.

## WebAPI

Schnittstelle, über die Programme einen Dienst über das Netz ansprechen.

## Werkstatt

Das Repo mit Wiki, Registern und voller Historie, in dem gearbeitet wird und aus dem das Produkt abgeleitet wird.

## Wiki

Sammlung verlinkter Dateien im Projekt, die Quelle der Wahrheit für Wissen und Festlegungen. An jedem Link steht, was dahinter wartet, damit der Agent nur liest, was er braucht.

## WorkspaceManager

Externes Programm, das Ausgangsdateien für den Agenten aufbereitet und Dokumente für den Versand erzeugt. Fehlt es, übernimmt der Agent beides.

## WSL

Teil von Windows, mit dem Linux-Programme unter Windows laufen.

## Zweck-Freigabe

Die Freigabe eines Freigabedokuments für genau einen Zweck, etwa für den nächsten Schritt, nicht für die Auslieferung.

## Zwei-Modelle-Regel

Je Prüfrunde mindestens zwei unabhängige Prüfer mit verschiedenen Modellen, jeder in frischem Kontext.

---

Zurück zum [Einstieg](../../README.md).
