# Ein Projekt aufsetzen

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `README.md`, `INIT.md`, `setup/init-frisch.sh`, `docs/Projektstart.md`, `wiki/Init-Choreografie.md`, `wiki/WorkspaceManager-Kontrakt.md`, `referenzprozesse/SP-1-Standardprozess/index.md`, `referenzprozesse/RP-1-Systementwicklung/index.md`; [clawbook-lehre](https://github.com/schlingensiepen/clawbook-lehre) `main`, `docs/README.md`, `docs/setup/kurs-dienste.md`, `vendor/wsm/wsm-1.1.1-py3-none-any.whl`.

Bis hierher trug die Lagerverwaltung die Beispiele. Ab jetzt kommt ein zweites Projekt dazu: DONE, eine Aufgabenverwaltung für mehrere Benutzer. An ihr sehen Sie, wie ein Projekt mit dem [Referenzprozess](../Z-anhang/Z010-glossar.md#referenzprozess) beginnt, einer Vorlage, die das Regelwerk, das vorbereitete Wiki und den Prozess für Softwareentwicklung mitbringt. Das Einrichten heißt im Regelwerk [Init](../Z-anhang/Z010-glossar.md#init). Sie geben einen Prompt, den Rest holt sich der Agent. Dabei stellt er Ihnen Fragen, und beim ersten Projekt kennen Sie die meisten davon noch nicht. Dieses Kapitel geht den Ablauf Schritt für Schritt mit und sagt je Frage, was sie bedeutet und was Sie für DONE antworten.

## Zwei Prompts für dasselbe Projekt

Im Teil [Beispiele](../Y-beispiele/README.md) stehen zwei Prompts für DONE nebeneinander. Der lange, [DONE ohne Regelwerk](../Y-beispiele/Y030-done-ohne-regelwerk.md), ist das Original aus der Zeit vor dem Referenzprozess. Er erklärt dem Agenten nicht nur, was DONE ist, sondern auch, wie er arbeiten soll: wohin er schreibt, wann er fragt, wie er Entscheidungen festhält. Das ist bei jedem neuen Projekt wieder fällig, und es ist bei jedem Projekt ein bisschen anders. Der kurze, [DONE mit Referenzprozess](../Y-beispiele/Y040-done-mit-referenzprozess.md), besteht aus drei Teilen: dem Startsatz, einer Erlaubnis zum Ausführen und der Beschreibung des Projekts.

Der Vergleich zeigt, was das Regelwerk dem Menschen abnimmt und was nur er sagen kann. Abgenommen wird alles, was von Projekt zu Projekt gleich ist: Ordner, Wiki, Register, Rückfrage-Regeln, Git, Prüfungen. Nur Sie können sagen, was das Projekt ist und für wen es ist. Das steht im kurzen Prompt, und mehr steht dort nicht. Er greift der Vorlage nichts vor. Die Fragen des Einrichtens stellt der Agent selbst, und Sie beantworten sie im Gespräch.

## Vorher: ein leerer Ordner

Im Terminal ist vorher nichts zu tun außer dem leeren Ordner. Sie legen ihn an, wechseln hinein und starten darin Ihren Agenten, wie im Kapitel [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md):

```bash
mkdir -p ~/source/sandbox/done
cd ~/source/sandbox/done
```

Sie brauchen dazu Git, einen Agenten, der Dateien von einer Repo-Adresse im Netz lesen darf, und beim Einrichten Internet. Ein Git-Repository müssen Sie nicht anlegen, das gehört zum Angebot des Agenten. Dann geben Sie den kurzen Prompt als erste Nachricht ein.

## Startsatz und Erlaubnis

Der erste Teil des Prompts ist ein Satz, den die Startseite des Referenzprozesses zum Kopieren anbietet:

```text
Richte dieses Verzeichnis als neues Projekt nach der Anleitung unter https://github.com/schlingensiepen/referenzprozess-softwareentwicklung ein.
```

Mehr braucht es nicht, damit der Agent loslegt. Er liest die Anleitung `INIT.md` direkt von der Repo-Adresse, bevor lokal irgendetwas liegt, und arbeitet sie ab. Drei Grundsätze stehen darin über allem. Nichts geht verloren: Nichts wird überschrieben oder gelöscht ohne Ihren ausdrücklichen Wunsch. Alles wird einsortiert: Vorgefundenes kommt in die Struktur oder wird verlinkt. Im Zweifel fragt er Sie.

Der zweite Teil des Prompts ist die Erlaubnis:

```text
git init, das Einbinden der Vorlage und das Kopieren der Projektdateien darfst du ausführen, jeweils auf dem Weg, den du empfiehlst.
```

Die Anleitung erlaubt dem Agenten diese drei Schritte nur nach Ihrer Zustimmung. Er soll sie anbieten, die genauen Befehle nennen und erst nach Ihrer Antwort handeln. Die Erlaubnis gibt die Zustimmung vorab, und sie legt sich auf keinen Weg fest. Sie sagt: Nimm, was du empfiehlst.

## Was der Agent zuerst tut

**Die Einbindung.** Als allererstes geht es darum, wie die Vorlage in Ihr Projekt kommt. Sie landet in beiden Fällen im Ordner `_template/` und wird dort nie verändert. Möglichkeit B ist die verknüpfte Vorlage, technisch ein [Submodul](../Z-anhang/Z010-glossar.md#submodul), das auf eine feste Version gepinnt ist und spätere Versionen gezielt nachziehen kann. Möglichkeit A ist die eingefrorene Kopie, eine Einmal-Kopie ohne Git-Verbindung, die zeigt, womit Sie gestartet sind. Die Anleitung empfiehlt B, und das passt für DONE. Stellt der Agent die Frage trotz der Erlaubnis, antworten Sie B. Fehlt ein Git-Repository, gehört `git init` zu diesem Schritt.

**Die Projektdateien.** Dann kopiert der Agent die Ausstattung der Vorlage ins Projekt. Dafür gibt es zwei Wege: das Kopier-Skript `sh _template/setup/init-frisch.sh` oder von Hand nach der Liste in der Anleitung. Die Anleitung empfiehlt das Skript. Kopiert werden das Regelwerk, eine `.gitignore`, die Liste der Dateien, die Git nicht aufnehmen soll, falls keine da ist, das komplette vorbereitete `wiki/` und der Arbeitsstand `devstate_active.md`. Diese Kopien sind lebende Dateien Ihres Projekts. Nie kopiert werden die Anleitungen, die Prozess-Vorlagen und die Erklärung für Menschen; die bleiben in `_template/` lesbar. Das Skript überschreibt nichts. Liegt im Ordner schon eine Datei gleichen Namens, lässt es sie aus und listet sie, und der Agent fragt Sie später, was damit geschehen soll.

**Der Aufnahme-Commit.** Den kopierten Inhalt committet der Agent als „Setup: Starter-Stand aufgenommen“. Das kündigt er an, fragt aber nicht. Es ist die einzige Ausnahme von der Regel, dass beim Einrichten nichts ohne Zustimmung ausgeführt wird.

## Der Fahrplan und das Briefing

Jetzt zeigt der Agent Ihnen einen Fahrplan: je Punkt eine Zeile mit dem, was feststeht oder ableitbar ist. Dazu bietet er den [Briefing-Modus](../Z-anhang/Z010-glossar.md#briefing-modus) an. Dann stellt er die Fragen einzeln, je Punkt mit einem kurzen Briefing. Die Alternative ist ein einziger nummerierter Block, je Punkt sein Vorschlag zuerst.

Der Rat für Ihr erstes Projekt lautet: Nehmen Sie das Briefing an. Ein Block setzt voraus, dass Sie schon wissen, was gefragt ist. Im Briefing erklärt der Agent die Sachlage, bevor Sie entscheiden, und Sie können bei jedem Begriff nachfragen. Wie das Briefing abläuft, steht im Kapitel [Entscheiden im Gespräch](../E-mensch-und-agent/E020-entscheiden-im-gespraech.md).

Was der Agent aus Ihrem Prompt oder aus Dateien im Ordner ableiten kann, fragt er nicht, sondern legt es als Entwurf vor. Was die Vorlage vorfestlegt, fragt er auch nicht. Dazu gehört, welche Register das Projekt am Anfang führt.

## Die Fragen des Einrichtens

Die Fragen stehen hier in der Reihenfolge der Anleitung. Einige kommen nur unter einer Bedingung, das ist jeweils gesagt.

**Passt der Prozess?** Die Vorlage bringt den Prozess für Softwareentwicklung mit. Der Agent fragt nur nach, wenn dieser Prozess nicht zum Vorhaben zu passen scheint oder wenn er unsicher ist. DONE ist Software. Kommt die Frage trotzdem, antworten Sie, dass der Software-Prozess richtig ist.

**Ein Repo oder zwei?** Die Frage legt fest, ob das Produkt ein eigenes [Repo](../Z-anhang/Z010-glossar.md#repo) bekommt. Zwei Repos braucht, wer die Arbeit und das vorzeigbare Produkt mit getrennten Historien führen will, etwa das Produkt öffentlich, die Arbeit privat. Für DONE antworten Sie: ein Repo. Warum man trennt, steht im Kapitel [Werkstatt, Produkt, Schleuse](../G-der-gesamtprozess/G030-werkstatt-produkt-schleuse.md).

**WorkspaceManager verfügbar?** Ein [WorkspaceManager](../Z-anhang/Z010-glossar.md#workspacemanager) ist ein eigenes Programm mit zwei Aufgaben: Es wandelt Originaldokumente in Text um, und es erzeugt Versanddateien wie PDFs. Es gehört nicht zur Vorlage. Der Agent fragt nach beiden Aufgaben, weil man die eine ohne die andere haben kann. Die Antwort lautet „beides vorhanden“, „nur Konvertierung“, „nur Outgoing-Erzeugung“ oder „keins“. Outgoing-Erzeugung ist die zweite Aufgabe, Konvertierung die erste. Was vorhanden ist, startet später nicht der Agent. Er bittet Sie, das Programm laufen zu lassen. Was fehlt, übernimmt er selbst.

Arbeiten Sie mit clawbook, haben Sie einen WorkspaceManager, denn der Projektverwalter `wsm` ist einer. Er übernimmt die Konvertierung, Versanddateien erzeugt er nicht (Stand Oktober 2026). Die Konvertierung läuft über den Befehl `wsm update`, der die Originale aus `raw/` als Text nach `input/` bringt. Dafür braucht `wsm` einen Server mit Docling, einem Dienst, der Dokumente in Markdown umwandelt. Dessen Adresse steht in der Datei `~/.workspacemanager.yml`, und nach dem ersten Start ist dort keine eingetragen. Ohne Eintrag fällt die Konvertierung aus. Antworten Sie also so:

- Mit clawbook und eingetragenem Docling-Server: „nur Konvertierung“.
- Mit clawbook ohne Docling-Server: „keins“.
- Ohne clawbook und ohne ein anderes solches Programm: „keins“.

Für DONE hängt an dieser Antwort am Anfang wenig. Es liegen noch keine Originale im Projekt, und auch der Agent wandelt nur um, was eine Aufgabe gerade braucht.

**Bearbeiter-Kürzel.** Das [Bearbeiter-Kürzel](../Z-anhang/Z010-glossar.md#bearbeiter-kürzel) sind drei Buchstaben, die in den Dateinamen versionierter Dokumente zeigen, wer sie bearbeitet hat. Der Agent selbst heißt dort `AIG`. Das Kürzel kann niemand ableiten, darum ist es eine echte Frage. Antworten Sie mit Ihrem eigenen Kürzel. Die Beispiele dieses Skripts schreiben dafür `MUS`.

**Commit-Sprache.** Die Frage legt die Sprache der [Commit](../Z-anhang/Z010-glossar.md#commit)-Nachrichten fest. Es gibt drei Möglichkeiten. A: alles in der Projektsprache. B: Die Sprache folgt dem, was geändert wurde, also Wiki und Dokumente in der Projektsprache, Code englisch. C: alles englisch. Die Buchstaben haben mit der Einbindung A und B nichts zu tun. Bei Codeprojekten ist B vorausgewählt, und für DONE nehmen Sie diese Vorauswahl. Die Projektsprache selbst ist mit Deutsch vorbelegt und keine Frage des Blocks.

**Prüfungen ohne zweites Modell.** Vor einer Freigabe prüft ein Prüfer in frischem Kontext, und das Prüf-Modell soll nicht das Bau-Modell sein. Diese Frage kommt nur, wenn der Agent in seiner Umgebung kein Werkzeug nennen kann, über das ein zweites Modell prüft. Dann braucht er einen Ersatzweg. Entweder prüft dasselbe Modell in frischem Kontext, der Ein-Modell-Weg, mit sichtbarer Einschränkung in der Freigabe. Oder Sie prüfen selbst. Für DONE nehmen Sie den Ein-Modell-Weg. Selbst zu prüfen setzt voraus, dass Sie wissen, worauf es ankommt, und das kommt erst im Kapitel [Prüfen](../G-der-gesamtprozess/G020-pruefen.md). Die Wahl hält der Agent in `Tools.md` fest.

**Rolle.** Ein Projekt ist Standalone, [Koordinator](../Z-anhang/Z010-glossar.md#koordinator) oder [Komponente](../Z-anhang/Z010-glossar.md#komponente); in der Frage schreibt der Agent „Komponent“. Vorausgewählt ist Standalone, ein einzelnes Repo. Für DONE passt Koordinator. DONE besteht aus einem [Backend](../Z-anhang/Z010-glossar.md#backend), dem Teil, der im Hintergrund auf einem zentralen Rechner läuft und die Daten hält, und mehreren Zugängen, und jeder Zugang soll später ein eigenes Projekt werden. Das Projekt, das ein System so zerlegt und die Teile wieder zusammenführt, ist der Koordinator. Das kann die Vorlage nicht wissen, darum steht es in der Beschreibung im Prompt. Der Agent legt die Rolle als abgeleitet vor, und Sie bestätigen sie. Er kündigt dann an, dass er das Verzeichnis der Schnittstellen zwischen den Teilen aktiviert. Wie das Zusammenspiel läuft, steht im Kapitel [Das Zusammenspiel](../H-mehrere-agenten/H040-das-zusammenspiel.md).

**Mission und Auftrag.** Das [Mission Statement](../Z-anhang/Z010-glossar.md#mission-statement) ist eine kurze Beschreibung, was ein Projekt ist und für wen. Für DONE ist es aus der Beschreibung im Prompt ableitbar. Der Agent legt deshalb einen Entwurf vor, statt zu fragen.

**Bezeichnung der ersten Marke.** Jedes Projekt arbeitet auf eine [Marke](../Z-anhang/Z010-glossar.md#marke) hin, ein benanntes Ergebnis, das nach außen geht. Der Agent schlägt „1.0“ vor, benannt „Erster Release“. Für DONE bestätigen Sie das. Die Marke steht vor dem ersten Eintrag, weil jeder Eintrag sie trägt. Was eine Marke ist, erklärt das Kapitel [Marken](../F-marken-und-freigaben/F010-marken.md).

**Remote-Ziel.** Ein Remote ist das Repo im Netz, in das die Commits geschoben werden. Das Anlegen haben Sie im Kapitel [Git als Gedächtnis](../A-verstehen-und-loslegen/A060-git-als-gedaechtnis.md) gesehen. Für DONE antworten Sie: ein privates Repo `done` auf GitHub. Der Agent richtet ein Remote nur auf diese Anweisung ein und schiebt nach seinem ersten eigenen Commit dorthin. Haben Sie GitHub noch nicht eingerichtet, antworten Sie: vorerst keins.

**Kollisionen.** Diese Frage kommt nur, wenn im Ordner schon eine Datei liegt, deren Name mit einer Datei der Vorlage kollidiert. In einem leeren Ordner kommt sie nicht vor.

**MADR.** Diese Frage steht nicht in der Liste der Anleitung. Sie kommt aus dem Software-Prozess, der sie als eigene Frage zum Einrichten mitbringt. [MADR](../Z-anhang/Z010-glossar.md#madr) ist ein festes Format, um Entscheidungen über den Aufbau einer Software aufzuschreiben. Die Frage lautet Ja oder Nein, voreingestellt ist Nein. Für DONE bleiben Sie bei Nein. Das Projekt hat mit dem Entscheidungs-Register schon einen Ort für Entscheidungen, und ein Ja legt nur die Form neuer Einträge fest.

## Die Umsetzung

Der Agent setzt die Antworten in fester Reihenfolge um: erst Kollisionen auflösen, dann die erste Marke anlegen, dann alles Weitere buchen, denn jeder neue Eintrag trägt die laufende Marke. Er schreibt einen Herkunfts-Vermerk ins Wiki, der sagt, aus welcher Vorlage in welcher Version das Projekt stammt. Er bucht Ihre Antworten und legt `Tools.md` mit den Prüfwerkzeugen an.

## Das Konzept-Angebot

Am Ende der Umsetzung macht der Agent ein Angebot. Er sichtet eine [Konzept-Sammlung](../Z-anhang/Z010-glossar.md#konzept-sammlung), eine Sammlung erprobter Vorgehensweisen in einem eigenen Repo. Welche Sammlung das ist, steht im Register der Vorlage, darum muss der Prompt sie nicht nennen. Der Agent markiert je Konzept, ob er es empfiehlt, ob es neutral ist oder ob es nicht relevant ist, und fragt, ob Sie weitere Sammlungen haben. Sie wählen konkrete Konzepte aus, antworten „später“ oder „nichts übernehmen“. Bei „später“ kommt das Angebot nach dem Mission Statement noch einmal. Wie aus dieser Auswahl Wissen im Projekt wird, zeigt das Kapitel [Wissen ins Projekt laden](D050-wissen-ins-projekt-laden.md).

Danach folgt der Dialog zum Mission Statement. Der Agent fragt, was hinein soll, und legt seinen Entwurf vor. Sie bestätigen, korrigieren oder ergänzen ihn.

## Der Abschluss

Der Agent schreibt seine Instruktionsdatei, einschließlich des Grundgesetzes aus dem Kapitel [Das Wiki](D010-das-wiki.md). Dann entstehen die Projekt-README und Ihre `TODO.md`, der Arbeitsstand wird nachgeführt, ein Prüfskript der Vorlage läuft ohne Fehler, und der Agent setzt den ersten eigenen Commit. Er meldet „Bereit für den ersten Auftrag.“ und wartet. Bei einem Softwareprojekt weist er zusätzlich auf den nächsten Schritt hin: eine Kette von Vorlagen, mit denen die technischen Grundentscheidungen geklärt werden, bevor die erste Fachlogik entsteht.

## Die Fachbegriffe im Prompt

Der dritte Teil des Prompts beschreibt, was DONE ist. Er enthält einige Begriffe, die der Agent kennt und Sie vielleicht noch nicht.

- [Getting Things Done](../Z-anhang/Z010-glossar.md#getting-things-done) ist eine Methode, Aufgaben aus dem Kopf in ein verlässliches System zu holen und zu ordnen; DONE setzt sie um.
- Das [Backend](../Z-anhang/Z010-glossar.md#backend) ist der Teil, der im Hintergrund auf einem zentralen Rechner läuft und die Daten hält, im Gegensatz zu den Oberflächen.
- Eine [WebAPI](../Z-anhang/Z010-glossar.md#webapi) ist die Schnittstelle, über die Programme das Backend über das Netz ansprechen.
- Eine [PWA](../Z-anhang/Z010-glossar.md#pwa) ist ein Programm, das im Browser läuft und sich wie eine App auf dem Telefon installieren lässt.
- Ein Kommandozeilen-Werkzeug bedient man im Terminal mit Befehlen, wie die Befehle aus dem Kapitel [Einen Agenten bekommen](../A-verstehen-und-loslegen/A030-einen-agenten-bekommen.md).
- Ein [MCP-Server](../Z-anhang/Z010-glossar.md#mcp-server) stellt einem Agenten nach einem festen Standard zusätzliche Tools zur Verfügung; DONE will so auch für Agenten bedienbar sein.

Der Prompt endet mit einer Aufforderung, die Sie in jeden Startprompt schreiben sollten: Was der Agent fachlich nicht versteht oder nur mit Annahmen umsetzen kann, soll er fragen, nach dem Einrichten. Vieles im Prompt ist bewusst oberflächlich geblieben. Das ist in Ordnung, solange der Agent weiß, dass er nachfragen darf.

## Was danach im Ordner liegt

Im Projekt liegen jetzt das Regelwerk, die Instruktionsdatei des Agenten, `Tools.md`, `TODO.md` und der Arbeitsstand, dazu `_template/` mit der Vorlage, die Standardordner und das `wiki/` mit allen Fassaden des Software-Prozesses. Von nun an beginnt jede Sitzung mit dem Sessionstart aus dem Kapitel [Regelwerk und Sessionstart](D020-regelwerk-und-sessionstart.md). Ein typischer erster Auftrag ist, sich den Fahrplan für die technischen Grundentscheidungen zeigen zu lassen. Sie können aber auch mit Material anfangen: Legen Sie Notizen oder Dokumente in `raw/`, und der Agent bietet beim nächsten Start an, sie ins Wiki zu übernehmen.

## Was jetzt klar sein sollte

- Ein Projekt beginnt mit einem leeren Ordner und einem Prompt. Die Anleitung liest der Agent selbst, und er führt nichts aus, wozu Sie nicht zugestimmt haben.
- Das Regelwerk nimmt Ihnen ab, was in jedem Projekt gleich ist. Sie sagen, was das Projekt ist.
- Der kurze Prompt greift der Vorlage nichts vor. Die Fragen stellt der Agent, und für das erste Projekt nehmen Sie sein Briefing an.
- Viele Fragen beantwortet der Vorschlag des Agenten oder die Beschreibung im Prompt. Das Kürzel kann nur von Ihnen kommen.
- Am Ende bietet der Agent an, erprobte Vorgehensweisen aus einer Sammlung zu übernehmen. Übernommen wird nur, was Sie wählen.
- Nach dem Einrichten gilt der normale Betrieb: Sessionstart, Züge, Commits.

Weiter mit [Register und Elemente](D040-register-und-elemente.md): warum eine Festlegung eine Nummer und eine Begründung bekommt und warum nichts gelöscht wird.
