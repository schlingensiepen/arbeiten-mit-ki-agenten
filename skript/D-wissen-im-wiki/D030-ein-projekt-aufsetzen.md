# Ein Projekt aufsetzen

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `README.md`, `INIT.md`, `setup/init-frisch.sh`, `docs/Projektstart.md`, `wiki/Init-Choreografie.md`.

Bis hierher trug die Lagerverwaltung die Beispiele. Ab jetzt kommt ein zweites Projekt dazu: DONE, eine Aufgabenverwaltung für mehrere Benutzer. An ihr sehen Sie, wie ein Projekt mit dem [Referenzprozess](../Z-anhang/Z010-glossar.md#referenzprozess) beginnt, einer Vorlage, die das Regelwerk, das vorbereitete Wiki und den Prozess für Softwareentwicklung mitbringt. Das Einrichten heißt im Regelwerk [Init](../Z-anhang/Z010-glossar.md#init). Sie geben einen Prompt, den Rest holt sich der Agent. Dieses Kapitel geht den Ablauf Schritt für Schritt mit und erklärt jede Entscheidung, die der Agent Ihnen dabei abverlangt.

## Zwei Prompts für dasselbe Projekt

Im Teil [Beispiele](../Y-beispiele/README.md) stehen zwei Prompts für DONE nebeneinander. Der lange, [DONE ohne Regelwerk](../Y-beispiele/Y030-done-ohne-regelwerk.md), ist das Original aus der Zeit vor dem Referenzprozess. Er erklärt dem Agenten nicht nur, was DONE ist, sondern auch, wie er arbeiten soll: wohin er schreibt, wann er fragt, wie er Entscheidungen festhält. Das ist bei jedem neuen Projekt wieder fällig, und es ist bei jedem Projekt ein bisschen anders. Der kurze, [DONE mit Referenzprozess](../Y-beispiele/Y020-done-mit-referenzprozess.md), besteht aus drei Teilen: einem Startsatz, einer Liste von Entscheidungen für das Einrichten und dem fachlichen Kern von DONE.

Der Vergleich zeigt, was das Regelwerk dem Menschen abnimmt und was nur er sagen kann. Abgenommen wird alles, was von Projekt zu Projekt gleich ist: Ordner, Wiki, Register, Rückfrage-Regeln, Git, Prüfungen. Nur der Mensch kann sagen, was das Projekt ist, für wen es ist und wie es betrieben werden soll. Genau das steht im kurzen Prompt.

## Vorher: ein leerer Ordner

Im Terminal ist vorher nichts zu tun außer dem leeren Ordner. Sie legen ihn an, wechseln hinein und starten darin Ihren Agenten, wie im Kapitel [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md):

```bash
mkdir done
cd done
```

Sie brauchen dazu Git, einen Agenten, der Dateien von einer Repo-Adresse im Netz lesen darf, und beim Einrichten Internet. Ein Git-Repository müssen Sie nicht anlegen; der Agent bietet es an. Mehr Vorbereitung verlangt der Referenzprozess nicht. Alles Weitere fragt er im Gespräch, und nur das, worüber Sie wirklich nachdenken müssen.

## Der Startsatz

Der erste Teil des kurzen Prompts ist ein Satz, den die Startseite des Referenzprozesses zum Kopieren anbietet:

```text
Richte dieses Verzeichnis als neues Projekt nach der Anleitung unter https://github.com/schlingensiepen/referenzprozess-softwareentwicklung ein.
```

Mehr braucht es nicht, damit der Agent loslegt. Er liest die Anleitung `INIT.md` direkt von der Repo-Adresse, bevor lokal irgendetwas liegt, und arbeitet sie ab. Drei Grundsätze stehen darin über allem: Nichts geht verloren, nichts wird überschrieben oder gelöscht ohne Ihren ausdrücklichen Wunsch. Alles wird einsortiert, Vorgefundenes kommt in die Struktur oder wird verlinkt. Im Zweifel fragt er Sie, gesammelt in einem Block.

## Was der Agent dann tut

**Die Einbindung.** Als allererste Frage will der Agent wissen, wie die Vorlage in Ihr Projekt kommt. Sie landet in beiden Fällen im Ordner `_template/` und wird dort nie verändert. Möglichkeit B ist die verknüpfte Vorlage, technisch ein Git-Submodul, das auf eine feste Version gepinnt ist und spätere Versionen gezielt nachziehen kann; sie ist empfohlen. Möglichkeit A ist die eingefrorene Kopie, eine Einmal-Kopie ohne Git-Verbindung, die zeigt, womit Sie gestartet sind. Fehlt ein Git-Repository, gehört `git init` zu diesem Angebot. Der Agent nennt die genauen Befehle und führt sie erst nach Ihrer Zustimmung aus.

**Die Projektdateien.** Dann bietet er zwei Wege an, die Ausstattung der Vorlage ins Projekt zu kopieren: das Kopier-Skript `sh _template/setup/init-frisch.sh` oder von Hand nach der Liste in der Anleitung. Kopiert werden das Regelwerk, eine `.gitignore`, falls keine da ist, das komplette vorbereitete `wiki/` und der Arbeitsstand `devstate_active.md`. Diese Kopien sind lebende Dateien Ihres Projekts. Nie kopiert werden die Anleitungen, die Prozess-Vorlagen und die Erklärung für Menschen; die bleiben in `_template/` lesbar. Das Skript überschreibt nichts. Liegt im Ordner schon eine Datei gleichen Namens, lässt es sie aus und listet sie, und der Agent fragt Sie später, was damit geschehen soll.

**Der Aufnahme-Commit.** Den kopierten Stand committet der Agent als „Setup: Starter-Stand aufgenommen“. Das kündigt er an, fragt aber nicht; es ist die einzige Ausnahme von der Regel, dass beim Einrichten nichts ohne Zustimmung ausgeführt wird.

**Der Fragen-Block.** Jetzt zeigt der Agent Ihnen zuerst einen Fahrplan: je Punkt eine Zeile, was feststeht, was er ableiten kann und was er fragen muss. Dazu bietet er den [Briefing-Modus](../Z-anhang/Z010-glossar.md#briefing-modus) an, in dem er jeden Punkt einzeln erklärt und mit Ihnen bespricht; die Alternative ist ein einziger nummerierter Block, je Punkt sein Vorschlag zuerst. Was er aus Ihrem Prompt oder aus Dateien im Ordner ableiten kann, fragt er nicht, sondern legt es als Entwurf vor. Was die Vorlage vorfestlegt, etwa den Software-Prozess, fragt er auch nicht.

**Die Umsetzung.** Der Agent setzt die Antworten in fester Reihenfolge um: erst Kollisionen auflösen, dann die erste Marke anlegen, dann alles Weitere buchen, denn jeder neue Eintrag trägt die laufende Marke. Er schreibt einen Herkunfts-Vermerk ins Wiki, der sagt, aus welcher Vorlage in welcher Version das Projekt stammt. Er bucht die Festlegungen aus dem Fragen-Block als Entscheidungen, legt `Tools.md` mit den Prüfwerkzeugen an, entwirft Mission Statement und Projektfakten und schreibt seine Instruktionsdatei, einschließlich des Grundgesetzes aus dem Kapitel [Das Wiki](D010-das-wiki.md).

**Der Abschluss.** Zuletzt entstehen die Projekt-README und Ihre `TODO.md`, der Arbeitsstand wird nachgeführt, ein Prüfskript der Vorlage läuft ohne Fehler, und der Agent setzt den ersten eigenen Commit. Dann meldet er „Bereit für den ersten Auftrag.“ und wartet. Bei einem Softwareprojekt weist er zusätzlich auf den nächsten Schritt hin: eine Kette von Vorlagen, mit denen die technischen Grundentscheidungen geklärt werden, bevor die erste Fachlogik entsteht.

## Die Entscheidungen im kurzen Prompt, Satz für Satz

Der zweite Teil des kurzen Prompts nimmt die Fragen des Blocks vorweg. Der Agent findet die Antworten im Prompt, legt sie als abgeleitet vor und fragt nur noch, was fehlt. Hier ist jede Zeile mit dem, was sie festlegt.

- **Einbindung: B, verknüpfte Vorlage. Git init und das Kopieren der Projektdateien darfst du ausführen.** Die verknüpfte Vorlage, weil Sie spätere Versionen der Vorlage nachziehen wollen. Der zweite Satz gibt die Zustimmung für die zwei Angebote vorweg, die der Agent sonst einzeln einholen würde; so läuft das Einrichten ohne Rückfrage bis zum Fragen-Block durch.
- **Ein Repo, kein Remote.** Zwei Repos braucht nur, wer die Arbeit und das vorzeigbare Produkt mit getrennten Historien führen will, etwa das Produkt öffentlich, die Arbeit privat. Für ein erstes Projekt genügt eines. Ohne Remote bleibt das Projekt vorerst auf Ihrem Rechner; ein Ziel im Netz lässt sich später einrichten. Warum man trennt, steht im Kapitel [Werkstatt, Produkt, Schleuse](../G-der-gesamtprozess/G030-werkstatt-produkt-schleuse.md).
- **Kein WorkspaceManager.** Ein [WorkspaceManager](../Z-anhang/Z010-glossar.md#workspacemanager) ist ein eigenes Programm, das Originaldokumente in Text umwandelt und Versanddateien wie PDFs erzeugt. Es gehört nicht zur Vorlage, und Sie haben keines. Fehlt es, übernimmt der Agent beides selbst. Die Antwort ist deshalb kurz: keins.
- **Bearbeiter-Kürzel: DON.** Das [Bearbeiter-Kürzel](../Z-anhang/Z010-glossar.md#bearbeiter-kürzel) sind drei Buchstaben, die in den Dateinamen versionierter Dokumente zeigen, wer sie bearbeitet hat. Der Agent selbst heißt dort `AIG`. Welche drei Buchstaben Sie wählen, kann niemand ableiten; darum ist es eine echte Frage.
- **Commit-Sprache: A, Projektsprache Deutsch.** Drei Möglichkeiten: A, alles in der Projektsprache; B, Wiki und Dokumente in der Projektsprache, Code englisch; C, alles englisch. Die Buchstaben haben mit der Einbindung A und B nichts zu tun. Die Projektsprache selbst ist mit Deutsch vorbelegt und keine Frage des Blocks.
- **Prüfungen: Ein-Modell-Weg, falls du kein zweites Modell erreichst.** Vor jeder Freigabe prüft ein Prüfer in frischem Kontext, und das Prüf-Modell soll nicht das Bau-Modell sein. Erreicht der Agent kein zweites Modell, braucht er einen Ersatzweg: dasselbe Modell prüft in frischem Kontext, mit sichtbarer Einschränkung in jeder Freigabe, oder Sie prüfen selbst. Warum zwei Modelle besser sind als eines, erklärt das Kapitel [Prüfen](../G-der-gesamtprozess/G020-pruefen.md).
- **Rolle: Koordinator.** Ein Projekt ist Standalone, [Koordinator](../Z-anhang/Z010-glossar.md#koordinator) oder Komponente. DONE besteht aus einem Backend und mehreren Zugängen, die später eigene Projekte werden können; das Projekt, das ein System so zerlegt und die Teile wieder zusammenführt, ist der Koordinator. Der Agent kündigt daraufhin an, dass er das Verzeichnis der Schnittstellen zwischen den Teilen aktiviert. Wie das Zusammenspiel läuft, steht im Kapitel [Das Zusammenspiel](../H-mehrere-agenten/H040-das-zusammenspiel.md).
- **Erste Marke: 1.0, Erster Release.** Jedes Projekt arbeitet auf eine [Marke](../Z-anhang/Z010-glossar.md#marke) hin, ein benanntes Ergebnis, das nach außen geht. Der Agent schlägt „1.0“ vor, Sie bestätigen oder nennen eine andere. Die Marke steht vor dem ersten Eintrag, weil jeder Eintrag sie trägt. Was eine Marke ist, erklärt das Kapitel [Marken](../F-marken-und-freigaben/F010-marken.md).
- **Keine Konzept-Sammlungen übernehmen, MADR nicht verwenden.** [Konzept-Sammlungen](../Z-anhang/Z010-glossar.md#konzept-sammlung) sind mitgelieferte Sammlungen erprobter Arbeitsweisen; der Agent sichtet sie und schlägt vor, welche zum Projekt passen. Für ein erstes Projekt gibt es noch nichts, was man übernehmen müsste, und das Angebot lässt sich jederzeit nachholen. [MADR](../Z-anhang/Z010-glossar.md#madr) ist ein festes Format, um Entscheidungen über den Aufbau einer Software aufzuschreiben; der Software-Prozess bietet es an. Das Projekt hat mit dem Entscheidungs-Register schon einen Ort für Entscheidungen, ein zweites Format kommt erst dazu, wenn es gebraucht wird.
- **Das Mission Statement leitest du aus dem Text unten ab, ich bestätige es dann.** Das [Mission Statement](../Z-anhang/Z010-glossar.md#mission-statement) ist eine kurze Beschreibung, was ein Projekt ist und für wen. Es ist aus dem fachlichen Kern ableitbar, also legt der Agent einen Entwurf vor, statt zu fragen.

Zwei Punkte des Blocks fehlen in der Liste, mit Absicht. Die Frage nach dem Prozess stellt der Agent nur, wenn das Vorhaben nicht nach Software aussieht; DONE ist Software. Und der letzte Absatz des Prompts beantwortet das Briefing-Angebot: „Was beim Einrichten noch offen ist, frag mich gesammelt in einem Block.“ Wann der Block und wann das Briefing die bessere Wahl ist, steht im Kapitel [Entscheiden im Gespräch](../E-mensch-und-agent/E020-entscheiden-im-gespraech.md).

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

- Ein Projekt beginnt mit einem leeren Ordner und einem Satz. Die Anleitung liest der Agent selbst, und er führt nichts aus, bevor Sie zugestimmt haben.
- Das Regelwerk nimmt Ihnen ab, was in jedem Projekt gleich ist. Sie sagen, was das Projekt ist, und treffen eine Handvoll Entscheidungen, die niemand ableiten kann.
- Der kurze Prompt nimmt diese Entscheidungen vorweg; jede Zeile hat einen Grund, und die meisten lassen sich später ändern.
- Nach dem Einrichten gilt der normale Betrieb: Sessionstart, Züge, Commits.

Weiter mit [Register und Elemente](D040-register-und-elemente.md): warum eine Festlegung eine Nummer und eine Begründung bekommt und warum nichts gelöscht wird.
