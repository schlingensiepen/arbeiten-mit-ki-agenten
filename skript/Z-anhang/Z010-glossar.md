# Glossar

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Begriffe.md`, `docs/Mehrere-Repos.md`, `MasterPrompt.md`; [peeragent](https://github.com/schlingensiepen/peeragent) `v0.2.0`, `docs/glossary.md`; [simple-a2a](https://github.com/schlingensiepen/simple-a2a) `v0.1.1`, `README.md`; [skill-a2a](https://github.com/schlingensiepen/skill-a2a) `v1.0.1`, `skills/a2a/SKILL.md`; [clawbook-lehre](https://github.com/schlingensiepen/clawbook-lehre) `main`, `docs/setup/kurs-dienste.md`; [proposals](https://github.com/schlingensiepen/proposals) `release/2026-11-02`, `README.md`.

Die Wörter dieses Skripts in je ein bis drei Sätzen, alphabetisch. Die Kapitel verlinken wichtige Fachbegriffe bei ihrer Einführung hierher. Wer von hier kommt, findet die Definition; der Zusammenhang steht im Kapitel, das den Begriff einführt. Englische Fachwörter, die im Deutschen üblich sind, bleiben stehen und werden erklärt. Wo das Regelwerk ein anderes Wort benutzt als das Skript, steht es dabei.

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

## Arbeitsbaum

Die Dateien eines Repos im Ordner, so wie sie gerade sind. Sauber ist der Arbeitsbaum, wenn nichts geändert ist, was nicht in einem Commit liegt.

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

## Contract

Wort des Regelwerks für eine vereinbarte Schnittstelle zwischen den Teilen eines Systems. Sie gehört dem Anbieter, im Regelwerk Provider, und der Koordinator führt sie im Verzeichnis der Schnittstellen.

## Datenmodell

Die Festlegung darüber, welche Arten von Dingen es gibt und welche Attribute und Beziehungen jede Art hat, im Beispiel der Lagerverwaltung: Ein Artikel hat eine Artikelnummer, eine Bezeichnung und einen Bestand und liegt an genau einem Lagerort. Es entsteht im Gespräch über die Anforderungen; die Daten kommen später, wenn das Programm läuft.

## Dokumentenkette

Der naive Ansatz: je Schritt der Softwareentwicklung ein Dokument, jedes baut auf dem vorigen auf.

## Einarbeiten

Die Befunde einer Prüfung in das geprüfte Dokument übernehmen. Das tut der Agent, danach folgt der Re-Check.

## Einfrieren

Der Inhalt eines Elements oder Dokuments wird ab einem Zeitpunkt nicht mehr geändert. Jede Änderung ergibt etwas Neues.

## Element

Nummerierter Eintrag in einem Register, etwa eine Anforderung oder eine Entscheidung. Es wird nicht überschrieben, sondern durch ein neues Element abgelöst, und geht in Freigabedokumente ein.

## Entscheidung

Festgelegte Projekt-Wahrheit mit Nummer, Wahl und Begründung. Sie kommt nur mit dem OK des Anwenders ins Register, ist ab dann eingefroren und wird nur durch eine neue Entscheidung abgelöst.

## Ersatzweg

Weg einer Prüfung, die ein zweites Modell verlangt, wenn kein Werkzeug ein zweites Modell bereitstellt: dasselbe Modell prüft in frischem Kontext, der Ein-Modell-Weg, mit sichtbarer Einschränkung in der Freigabe, oder ein Mensch prüft. Der Anwender wählt ihn beim Aufsetzen des Projekts.

## Fassade

Übersichtsdatei im Wiki, am Stück lesbar, je Thema genau eine.

## Festlegung

Etwas, das in einem Projekt gilt und nicht mehr offen ist. Inhaltliche Festlegungen trifft der Mensch; sie kommen als Entscheidung mit Nummer und Begründung ins Register.

## Freezer

Etwas, das einfriert. Das Freigabedokument ist Sammler und Freezer: Es stellt die Elemente einer Marke zusammen und friert sie als Ganzes ein.

## Freigabe

Die Erklärung, dass ein Freigabedokument für einen bestimmten Zweck verlässlich ist, gebucht als Entscheidung in der Form „Stand x von ⟨Artefakt⟩, freigegeben für Zweck Z [zu Marke M]“. Der Zusatz steht, wenn die Marke nicht die laufende ist oder es kein Freigabedokument gibt. Sie wird nie zurückgenommen, eine Änderung ergibt ein neues Dokument mit neuer Freigabe.

## Freigabedokument

Allgemeinverständlicher Name für einen Stand: Das Dokument sammelt die Elemente einer Marke und friert sie ein, damit eine Freigabe etwas Festes hat, worauf sie sich bezieht.

## Getting Things Done

Methode, Aufgaben aus dem Kopf in ein verlässliches System zu holen und zu ordnen. Sie ist die Grundlage des Beispiels DONE.

## Gewichte

Die Zahlen in einem Modell, die beim Training angepasst werden. Sie sind das, was das Modell gelernt hat.

## gh

Das Kommandozeilen-Werkzeug von GitHub. Es legt zum Beispiel mit `gh repo create` ein Repo auf GitHub an.

## Git

Programm, das die Geschichte eines Projekts aufzeichnet: Jede Änderung bleibt nachvollziehbar und lässt sich zurücknehmen.

## GitHub

Dienst im Netz, auf dem Git-Repos liegen, gesichert und für andere erreichbar.

## Git-Tag

Siehe Tag.

## Harness

Das Programm um das Sprachmodell herum: Es legt dem Modell den Kontext vor, führt dessen Tool-Aufrufe aus und steckt die Ergebnisse in den nächsten Prompt. Das Wort heißt wörtlich Zaumzeug: Der Harness führt das Modell, ohne selbst klug zu sein.

## Hauptzweig

Die eine Fassung eines Projekts, an der alle arbeiten und aus der geliefert wird.

## Inbox

Englisch für Postfach, siehe dort. Im Beispiel DONE heißt Inbox etwas anderes: die Ablage für Aufgaben ohne Tag, nach der Methode Getting Things Done. Beide haben nur das Wort gemeinsam.

## Init

Das einmalige Einrichten eines neuen Projekts aus dem Referenzprozess, in dem der Agent die Festlegungen abfragt, die er nicht ableiten kann.

## Instruktionsdatei

Die agent-spezifische Datei, die der Agent beim Start automatisch lädt, etwa `CLAUDE.md`. Weil jedes Wort darin Kontext kostet, bleibt sie klein.

## Kardinalität

Die Anzahl auf einer Seite einer Beziehung zwischen zwei Dingen im Modell: eins oder viele. Ob ein Artikel an einem Lagerort liegt oder an mehreren, ist eine Frage der Kardinalität, und die Antwort gibt der Anwendungsfall.

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

Sammlung erprobter Arbeitsweisen in einem eigenen Repo. Der Agent schlägt beim Einrichten vor, was zum Projekt passt, und übernimmt nur, was der Mensch auswählt.

## Koordinator

Das Projekt, das ein System in Komponenten zerlegt und deren Lieferungen integriert.

## Langfristiger Ansatz

Eine Arbeitsweise, die über Wochen, über viele Sitzungen und über mehrere Versionen trägt: Wissen im Wiki, Entscheidungen beim Menschen, Schnitt nach Marken, unabhängige Prüfung und ein vom Arbeitsmaterial getrenntes Produkt. Gegenstück zum naiven Ansatz.

## Lieferung

Der Git-Tag einer Komponente: das Ergebnis, das sie dem Koordinator als Nachricht meldet und das er an der Marke bucht.

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

Das Modell des Modells, eine Ebene über dem Datenmodell. Es legt fest, woraus ein Datenmodell bestehen kann: aus Arten von Dingen, ihren Attributen und ihren Beziehungen.

## Migration

Sonderweg, der ein bestehendes Projekt ohne Regelwerk nachträglich unter das Regelwerk bringt.

## Mission Statement

Kurze Beschreibung, was ein Projekt ist und für wen.

## Modell

Der Ausschnitt der Realität, den eine Software abbildet, so genau, wie der Anwendungsfall es braucht, und nicht genauer. Das Modell steht für die Realität, es ist nicht die Realität. Daneben sagt das Skript kurz Modell, wenn es das Sprachmodell meint.

## Nachricht

Text, den ein Agent einem anderen schickt; er liegt im Postfach, bis der Empfänger hineinsieht. Im Regelwerk die Datei in `output/nachrichten/` des Absenders, mit der ein Repo einem anderen etwas mitteilt, etwa eine Lieferung oder einen Änderungswunsch; sie ist ab der Anlage eingefroren, ein Werkzeug kann ihren Inhalt zustellen, und der Empfänger bucht daraus in seine eigenen Register. Nicht gemeint sind eine Commit-Nachricht und ein Versand an Menschen.

## Nachrichten-Wächter

Wort des Regelwerks für eine Prüfung, die der Agent jedes Projekts beim Sessionstart, täglich und bei jeder eingegangenen Nachricht ausführt: Sind eigene Nachrichten noch ohne Quittung, sind an ihn gerichtete noch nicht gebucht? Er meldet, er blockiert nicht.

## Nachweis

Eintrag in einem Register, der nie abgelöst, sondern nur mit Vermerken ergänzt wird: der Bericht eines Prüfers, ein Rechercheergebnis, ein eingegangenes Dokument. Gegenstück zum Element.

## Naiver Ansatz

Der direkte Weg von den Anforderungen zum Programm, mit einem Agenten, ohne Regelwerk und ohne Vorlage, je Schritt ein Dokument. Er scheitert nicht an einem Fehler, sondern an Ursachen, die beim ersten Durchlauf unsichtbar sind.

## peeragent

Werkzeug, das einen zweiten Agenten als eigenen Prozess in einer tmux-Sitzung startet.

## Phase

Wort des Regelwerks für einen Schritt des Gesamtprozesses, etwa Anforderungen sammeln oder Testen. Phasen ordnen Freigaben, nicht Arbeit.

## Planmodus

Betriebsart, in der der Agent erst einen Plan vorlegt, statt zu handeln. Der Harness sagt dem Modell, dass es planen soll, und sperrt in Claude Code das Ändern (Stand Oktober 2026).

## Postfach

Der Eingang, in dem die Nachrichten für einen Agenten liegen, bis er hineinsieht; englisch Inbox. Je Team hat jeder Agent genau eines. Auf dem einfachen Weg ist es ein Verzeichnis, sonst führt es der Dienst simple-a2a.

## Produkt

Das, was eine Marke hervorbringt und nach außen geht, bei Software der Code mit seinen Tests. Es wird nicht als Dokument eingefroren, sondern mit einem Git-Tag markiert. Liegt es in einem eigenen Repo, heißt dieses Produkt-Repo, im Gegensatz zur Werkstatt.

## Prompt

Der Text, der dem Sprachmodell vorgelegt wird; im engeren Sinn die Eingabe des Menschen.

## Prozess

Die Folge der Phasen, die ein Projekt von der ersten Anforderung bis zur Auslieferung durchläuft, jede als Tätigkeit benannt und jede mit einem Freigabedokument als Ergebnis, das Ausarbeiten mit dem Git-Tag auf dem Produkt. Die Phasen sind ein Angebot und eine Checkliste, kein Zwang.

## Prüfer

Wer ein Ergebnis beurteilt, ohne daran mitgeschrieben zu haben: ein Subagent in frischem Kontext, ein zweiter Agent oder ein Mensch. Sein Ergebnis ist ein Bericht mit Befunden und einer Ampel.

## Prüfkette

Die Folge der Freigabedokumente einer Marke, in der jedes vor seiner Freigabe gegen seine freigegebenen Vorgänger geprüft wird: auf Widerspruch, Abdeckung und Unbegründetes. Das Regelwerk nennt sie Kette, die einzelne Prüfung Kettenprüfung. Nicht gemeint sind die Runden aus Prüfen, Einarbeiten und Re-Check.

## PWA

Programm, das im Browser läuft und sich wie eine App auf dem Telefon installieren lässt.

## Raster

Marken als Zeilen, Phasen als Spalten, je Feld ein Freigabedokument. Aus der Dokumentenkette des naiven Ansatzes wird so ein Raster. Nicht gemeint ist das Antwort-Raster.

## Realm

Bei simple-a2a der abgegrenzte Bereich, in dem Teams und Agenten zusammenarbeiten.

## Reasoning

Fähigkeit eines Sprachmodells, vor der Antwort Zwischenschritte zu schreiben und so eine Aufgabe in Stufen zu lösen. Für den Agenten zählt, dass man das Modell damit nach dem nächsten Schritt fragen kann statt nach der Antwort.

## Re-Check

Erneute Prüfung, nachdem die Befunde einer Prüfung eingearbeitet sind.

## Referenzprozess

Im Skript kurz für den Referenzprozess Softwareentwicklung, die öffentliche Vorlage für Softwareprojekte mit Regelwerk, vorbereitetem Wiki und Anleitungen für neues Projekt, Migration und Upgrade. Genau genommen belegt ein Referenzprozess die Phasen für eine Projektart; der für Softwareentwicklung ist in der Vorlage schon eingespielt.

## Regelwerk

Die Dateien, die festlegen, wie ein Agent in einem Projekt arbeitet, mit dem MasterPrompt als Quelle aller Regeln.

## Register

Übersichtsdatei im Wiki mit nummerierten Einträgen, etwa Entscheidungen oder Anforderungen.

## Remote

Das Repo im Netz, in das die Commits geschoben werden, etwa auf GitHub.

## Repo

Kurz für Repository: ein Projektordner unter der Aufsicht von Git mit seiner ganzen Geschichte.

## Review

Prüfdurchgang mit frischem Kontext, der einen Bericht und ein Urteil ergibt. Wer geprüft hat, hat nicht mitgeschrieben.

## Rolle

Die Stellung eines Projekts in einem System: Standalone, Koordinator oder Komponente. Standalone ist ein einzelnes Repo ohne Zerlegung und beim Einrichten vorausgewählt. Daneben spricht das Skript von den Rollen von Mensch und Agent: Der Mensch entscheidet, der Agent leitet ab, legt vor und führt aus.

## Rücklauf

Nachricht des Koordinators an die betroffenen Komponenten, wenn eine Änderung seine Grundlagen betrifft, also Funktionsbeschreibung, Zuschnitt der Komponenten oder Übergabe. Die Freigabedokumente einer Komponente, die auf das alte Übergabe-Dokument verweisen, sind damit überholt.

## Sammler

Das Freigabedokument in seiner ersten Aufgabe: Es stellt die angenommenen Elemente einer Marke zusammen und verweist auf sie, ohne sie zu kopieren. Siehe Freezer.

## Schleuse

Der geregelte Übergang von der Werkstatt ins Produkt: Kleinteilige Dokumente werden zu in sich vollständigen, und was nicht nach außen gehört, bleibt zurück. Es gibt sie erst bei zwei Repos, und sie ist kein Programm, sondern eine Regel.

## selbsttragend

Eigenschaft eines Dokuments, das am Stück an einen Empfänger ohne Zugang zum Wiki weitergegeben wird: keine Wikilinks, keine Register-Nummern, Begründungen ausgeschrieben. Gegenstück ist ein Dokument, das nur mit dem Wiki lesbar ist, weil es verlinkt statt wiederholt.

## Sessionstart

Der feste Ablauf zu Beginn jeder Sitzung: Der Agent orientiert sich, lädt den nötigen Kontext, sucht, was liegen geblieben ist, und meldet sich bereit.

## Shell

Programm, das Befehle in einem Terminal entgegennimmt und ausführt.

## simple-a2a

Kleines Protokoll, mit dem Agenten einander adressierte Nachrichten schicken. Der gleichnamige Dienst ist das Postamt dazu: Er befördert und bewahrt die Nachrichten und prüft, von wem sie kommen.

## Sitzung

Eine zusammenhängende Arbeit mit einem Agenten, von seinem Start bis zum Ende, mit einem eigenen Kontext.

## Skill

Anleitung für eine bestimmte Art von Aufgabe, die der Agent bei Bedarf in den Kontext lädt. Technisch ein weiteres Stück Prompt. Wer keine Mail verschickt, liest den Mail-Skill nicht; so bleibt das Fenster frei.

## skill-a2a

Skill, der Agenten auf demselben Rechner unter demselben Benutzerkonto beibringt, einander Nachrichten als Dateien zu schicken. Im Skript ist das der einfache Weg; der Absender ist dabei nicht geprüft.

## Skip Permissions

Berechtigungsstufe, bei der der Agent ohne jede Rückfrage handelt. Nur auf einem wegwerfbaren Rechner ohne wertvolle Zugänge oder Daten und mit per Git gesicherter Arbeit.

## Sonderweg

Weg neben dem Projektstart aus der Vorlage, für Projekte, die schon da sind: die Migration für ein Projekt ohne Regelwerk, das Upgrade für ein Projekt mit einer älteren Version der Vorlage.

## Spezifikation

Eine Bauanleitung, so genau, dass jemand danach programmieren kann, der das Grundproblem nicht kennt.

## Sprachmodell

Siehe LLM.

## Stand

Wort des Regelwerks und der Bilder für das, was das Skript Freigabedokument nennt: ein Dokument, das zu einer Marke aus eingefrorenen Elementen gebildet wird und eine Freigabe trägt. Jede Änderung ergibt ein neues Dokument mit neuer Versionsnummer, das alte bleibt liegen. Nicht gemeint sind Angaben wie „Stand Oktober 2026“ und „Stand der Quellen“ und die Datumszeile einer lebenden Datei, im Regelwerk Bearbeitungsstand.

## Standardaufgabe

Mechanisch festgelegter Vorgang, etwa ein Commit, den der Agent ohne Rückfrage ausführt, weil die Regeln vollständig feststehen.

## Standard-Modus

Grundeinstellung des Agenten: Bei Unklarheit fragt er nach und führt nicht aus. Das gilt besonders für inhaltliche Entscheidungen und alles mit Außenwirkung.

## Startprompt

Der erste Prompt, mit dem ein Agent ein Vorhaben beginnt. Dazu zählt auch die Datei, die ein Koordinator für den Agenten einer neuen Komponente erzeugt.

## Start-Tabelle

Liste, die der Agent eines Koordinators vor dem Start der Komponenten zur Entscheidung vorlegt: je Komponente Name, Repo-Name, lokaler Pfad, Remote und Übernahme-Art.

## Subagent

Hilfs-Agent, den ein Agent mit eigenem, frischem Kontext für einen abgegrenzten Auftrag startet; zurück kommt nur sein Ergebnis. Im Regelwerk auch Unteragent.

## Submodul

Ein Repo, das als Unterordner in einem anderen Repo liegt und dort auf einen festen Commit zeigt. So liegt die Vorlage im Projekt oder das Produkt-Repo in der Werkstatt.

## Systemprompt

Der Teil des Prompts, den der Harness vorgibt: Er legt fest, wie sich das Modell verhält und dass es statt einer Antwort Tool-Aufrufe zurückgeben kann.

## Tag

In Git eine Markierung an einem bestimmten Commit, die einen Namen trägt; das Skript schreibt dafür Git-Tag. Das Produkt einer Marke wird so markiert, und ein Git-Tag wird nie verschoben und nie gelöscht. Im Beispiel DONE heißt Tag etwas anderes, ein Schlagwort an einer Aufgabe; beide haben nur das Wort gemeinsam.

## Team

Eine Gruppe von Agenten, die einander Nachrichten schicken. Das Team hat einen Namen, und jeder Agent darin hat einen Namen. Beim Dienst simple-a2a liegt es in einem Realm.

## Terminal

Fenster, in dem man Befehle tippt. Die Shell läuft darin und führt sie aus.

## tmux

Programm, das Terminal-Sitzungen vom Fenster löst, sodass ein Agent eine getrennte Verbindung überlebt.

## tmux-helper

Windows-Programm, das die tmux-Sitzungen entfernter Rechner auflistet und als Tabs im Windows Terminal öffnet.

## Token

Die Einheit, in der ein Sprachmodell Text zerlegt, etwa ein Wort oder ein Wortteil; lange zusammengesetzte Wörter werden in mehrere Tokens zerlegt. Kontextfenster und Kosten werden in Tokens gemessen. Mit dem Zugangstoken hat es nur das Wort gemeinsam.

## Tool

Fähigkeit, die der Harness dem Modell anbietet, etwa eine Datei lesen, einen Befehl ausführen oder im Web recherchieren. Ein Tool ist gewöhnliche Software: Text und Parameter hinein, Text heraus.

## Tool-Aufruf

Markierung im Text des Modells, die ein Tool anfordert. Das Modell führt nichts aus, der Harness tut es und gibt das Ergebnis zurück.

## Übergabe

Was ein Koordinator einer Komponente mitgibt: ein freigegebenes Freigabedokument, auf das sich die Komponente stützt und das die Wurzel ihrer Kette ist. Das Regelwerk nennt es Übergabe-Stand, das Skript auch Übergabe-Dokument. Nicht gemeint ist das Weitergeben der Arbeit am Ende einer Sitzung.

## Übernahme-Art

Wo die Arbeit einer Komponente beginnt. Selbstständig, der Standard: Sie sammelt eigene Anforderungen und schreibt ihre eigene Funktionsbeschreibung. Auftrag: Der Koordinator beschreibt die Funktion und übergibt sie, die Komponente beginnt mit dem Zerlegen.

## Unteragent

Siehe Subagent.

## Upgrade

Sonderweg, der ein Projekt aus der Vorlage auf deren neue Version hebt.

## Vertrauensabfrage

Frage des Agenten beim ersten Start in einem Ordner, ob er diesem Ordner trauen soll.

## Verwerfen

Ein Element wird mit Begründung aufgegeben, ohne Nachfolger. Es bleibt sichtbar stehen.

## Verzicht

Bewusstes Auslassen einer Phase samt ihrem Freigabedokument für eine Marke, als Entscheidung gebucht. Für diese Marke entfallen damit das Dokument und seine Prüfpflichten.

## Veto

Widerspruch des Menschen gegen etwas, das der Agent angekündigt oder ohne Rückfrage erledigt hat. Damit lässt sich etwa eine Standardaufgabe zurücknehmen.

## Vorfestlegung

Was die Antwort auf eine Frage für andere Fragen schon mitentscheidet. Der Agent stellt zuerst die Frage mit der stärksten Vorfestlegung; Folgefragen entfallen dann oder werden ableitbar. Was die Vorlage vorfestlegt, fragt er gar nicht.

## Vorlage

Fertige Ausstattung für ein neues Projekt mit Regelwerk, vorbereitetem Wiki und Prozess. Sie liegt im Projekt im Ordner `_template/` und wird dort nie verändert. Im Skript ist das der Referenzprozess Softwareentwicklung, das Regelwerk nennt sie auch Starter.

## WebAPI

Schnittstelle, über die Programme einen Dienst über das Netz ansprechen.

## Werkstatt

Der Ort der Arbeit mit Wiki, Registern und voller Historie, aus dem das Produkt hervorgeht. Im Skript gibt es sie in jedem Projekt; bei einem Repo liegt sie mit dem Produkt im selben Repo. Das Regelwerk ist enger: Es benutzt das Wort nur für zwei Repos und sagt bei einem Repo einfach Wiki.

## Wiki

Sammlung verlinkter Dateien im Projekt, die Quelle der Wahrheit für Wissen und Festlegungen. An jedem Link steht, was dahinter wartet, damit der Agent nur liest, was er braucht.

## WorkspaceManager

Externes Programm mit zwei Aufgaben: Es wandelt Originaldokumente in Text um und erzeugt Versanddateien wie PDFs. Was fehlt, übernimmt der Agent. In clawbook ist der Projektverwalter `wsm` ein WorkspaceManager; er übernimmt nur die Umwandlung und braucht dafür einen Docling-Server (Stand Oktober 2026).

## WSL

Teil von Windows, mit dem Linux-Programme unter Windows laufen.

## Zugangstoken

Geheime Zeichenfolge, mit der sich ein Agent beim Dienst simple-a2a ausweist. Sie steht für genau einen Namen in genau einem Team. Mit den Tokens, in die ein Sprachmodell Text zerlegt, hat sie nur das Wort gemeinsam.

## Zweck-Freigabe

Die Freigabe eines Freigabedokuments für genau einen Zweck, etwa für den nächsten Schritt, nicht für die Auslieferung.

## Zwei-Modelle-Regel

Je Prüfrunde mindestens zwei unabhängige Prüfer mit verschiedenen Modellen, jeder in frischem Kontext.

---

Zurück zum [Einstieg](../../README.md).
