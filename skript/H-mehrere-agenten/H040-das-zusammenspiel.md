# Das Zusammenspiel

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Mehrere-Repos.md`, `Vorgehen.md`; [peeragent](https://github.com/schlingensiepen/peeragent) `v0.2.0`, `README.md`; [simple-a2a](https://github.com/schlingensiepen/simple-a2a) `v0.1.1`, `README.md`; [skill-a2a](https://github.com/schlingensiepen/skill-a2a) `v1.0.1`, `skills/a2a/SKILL.md`.

DONE besteht aus einem Backend und fünf Zugängen. Ein Agent müsste das alles in einem [Kontextfenster](../Z-anhang/Z010-glossar.md#kontextfenster) halten, und das Fenster ist begrenzt. Also schneidet man: Bei drei Teilen sind es drei Fenster und drei Agenten, und jeder hält nur seinen Teil. Das löst das Platzproblem und schafft ein neues. Niemand sieht mehr das Ganze, und die Teile müssen am Ende zusammenpassen. Die drei Kapitel davor haben die Werkzeuge gebracht. Dieses Kapitel setzt sie zusammen, in drei Schritten: erst die Rollen, dann der Start, zuletzt der Rückweg.

## Schritt 1: Koordinator und Komponenten

Das Projekt, das ein System zerlegt, heißt [Koordinator](../Z-anhang/Z010-glossar.md#koordinator). Jeder Teil, der dabei ein eigenes Projekt wird, heißt [Komponente](../Z-anhang/Z010-glossar.md#komponente). Eine Komponente ist kein Ordner im Koordinator. Sie hat ein eigenes [Repo](../Z-anhang/Z010-glossar.md#repo) und wendet das ganze Vorgehen selbst an, mit eigenem Wiki und eigenem Agenten. Im Regelwerk geschieht dieser Schritt in der Phase P6, Starten von Teilaktivitäten, die Sie aus dem Kapitel [Softwareentwicklung als Prozess](../G-der-gesamtprozess/G010-softwareentwicklung-als-prozess.md) kennen.

Bei DONE steht das schon im Startprompt aus [DONE mit Referenzprozess](../Y-beispiele/Y040-done-mit-referenzprozess.md):

```text
Jeder Zugang soll später ein eigenes Projekt werden, dieses Projekt ist der Koordinator.
```

Fünf Zugänge ergeben fünf Komponenten: Kommandozeile, Mobile-App, Desktop-App, MCP-Server und Messenger-Bot. Das Backend ist kein Zugang. Es bleibt im Projekt DONE, der Koordinator hat hier also auch ein eigenes Bauteil.

![Oben ein breiter blauer Block Koordinator DONE mit dem Zusatz: zerlegt, führt zusammen, baut das Backend. Darunter fünf grüne Blöcke, jeder mit dem Zusatz Komponente: Kommandozeile, Mobile-App, Desktop-App, MCP-Server und Messenger-Bot. Von oben führt ein schwarzer Pfeil zu jeder Komponente, einer davon ist mit Übergabe beschriftet.](bilder/H040-gesamtbild-1.svg)

**Koordinator und Komponenten.** Das Projekt DONE ist der Koordinator, jeder Zugang wird eine Komponente. Jede Komponente bekommt vom Koordinator eine Übergabe.

Bevor eine Komponente startet, legt Ihnen der Agent die nötigen Entscheidungen vor. Von selbst beginnt er nicht. Die erste ist die Start-Tabelle: je Komponente Name, Repo-Name, lokaler Pfad, Remote und Übernahme-Art. Für den Repo-Namen schlägt er `<projekt>-<komponente>` vor, als Ablage ein Verzeichnis neben dem Koordinator. Für DONE könnte die Tabelle so aussehen; das Remote ist hier weggelassen, die Werte sind ein Beispiel:

| Komponente | Repo | Verzeichnis | Übernahme-Art |
|---|---|---|---|
| Kommandozeile | `done-cli` | `~/source/sandbox/done-cli` | Auftrag |
| Mobile-App | `done-mobil` | `~/source/sandbox/done-mobil` | selbstständig |
| Desktop-App | `done-desktop` | `~/source/sandbox/done-desktop` | selbstständig |
| MCP-Server | `done-mcp` | `~/source/sandbox/done-mcp` | Auftrag |
| Messenger-Bot | `done-bot` | `~/source/sandbox/done-bot` | selbstständig |

Die Übernahme-Art sagt, wo die Arbeit der Komponente beginnt. **Selbstständig** ist der Standard: Die Komponente sammelt eigene Anforderungen, die auf die Funktionsbeschreibung des Koordinators verweisen, und schreibt ihre eigene Funktionsbeschreibung. Das passt zu einem Teil mit eigenem Inhalt. **Auftrag** heißt: Der Koordinator beschreibt die Funktion und übergibt sie, die Komponente beginnt mit dem Zerlegen. Das passt zu einer klar umrissenen Arbeit. Der Agent schlägt eine Art vor und nennt Vor- und Nachteile. Sie wählen, und die Wahl wird als Entscheidung gebucht.

Was im Bild Übergabe heißt, ist ein freigegebenes [Freigabedokument](../Z-anhang/Z010-glossar.md#freigabedokument) des Koordinators. Das Regelwerk nennt es Übergabe-Stand. Es ist die Wurzel der Kette der Komponente: Worauf sich die Komponente stützt, steht dort. Bei beiden Arten führt sie ihre Kette bis zum Testen. Ihr Git-[Tag](../Z-anhang/Z010-glossar.md#tag) ist ihre Lieferung. Danach bildet sie einen Testplan und belegt den Durchgang mit einem Testbericht.

Der Koordinator führt die Lieferungen zusammen. Sein Testplan setzt den eigenen Tag voraus, bei DONE den des Backends, und alle Lieferungen. Den Integrationstest des Gesamtsystems führt er. Auslieferung und Deployments liegen ebenfalls bei ihm, außer eine Komponente hat eine eigene Zielumgebung.

Eine Regel hält die Projekte auseinander: Jedes Repo schreibt nur sein eigener Agent. Lesen beim Nachbarn ist erlaubt, in beide Richtungen. Der Agent der Mobile-App darf also im Wiki des Koordinators nachlesen, aber er ändert dort nichts. Zwei Agenten bearbeiten deshalb nie dasselbe Repo.

## Schritt 2: peeragent und tmux

Die Komponente hat noch keinen Agenten. Der Koordinator erzeugt dafür in seinem Ordner `output/` einen [Startprompt](../Z-anhang/Z010-glossar.md#startprompt), eine Markdown-Datei. Sie beginnt mit demselben Start-Satz wie der Prompt von DONE, denn auch die Komponente wird ein neues Projekt aus derselben Vorlage. Dazu nennt sie die Rolle Komponente, Name, Pfad und Remote des neuen Repos, Name und Pfad des Koordinators, die Übernahme-Art, das Übergabe-Dokument, die bekannten Nachbarn und die Wahl für Start und Transport. Den Prozess gibt sie nicht vor. Was der Startprompt festlegt, fragt der Agent der Komponente nicht mehr; alles andere läuft wie im Kapitel [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md).

Die letzte Angabe ist die zweite Entscheidung, die der Agent Ihnen vorlegt: Wie wird der Agent der Komponente gestartet, und wie laufen die Nachrichten zwischen den Repos? Es gibt zwei gleichwertige Wege. Ohne Werkzeug liest der Empfänger die Nachricht beim Absender, den Anstoß geben Sie oder eine regelmäßige Prüfung, die weiter unten vorkommt. Mit Werkzeug startet ein Agent den anderen, und ein zweites Werkzeug stellt die Nachrichten zu. Das Regelwerk empfiehlt dafür peeragent für den Start und simple-a2a oder skill-a2a für den Transport. Es ist die einzige Stelle, an der es Produkte empfiehlt. Dieses Kapitel geht den Weg mit Werkzeug, weil er die Werkzeuge dieses Teils zusammenführt.

Der Startprompt ist eine Datei. Das ist genau die Form, die [peeragent](H020-peeragent.md) verlangt: Der Prompt beim Start ist nur ein Zeiger. Für die Kommandozeile sieht das so aus, der Name der Datei in `output/` ist ein Beispiel:

```bash
mkdir -p ~/source/sandbox/done-cli
cat > ~/source/sandbox/done-cli/.peeragent-prompt.txt <<EOF
Lies $HOME/source/sandbox/done/output/startprompt-done-cli.md und führe ihn aus.
EOF
peeragent start agent --folder ~/source/sandbox/done-cli --harness claude --prompt-file ~/source/sandbox/done-cli/.peeragent-prompt.txt
```

Diese Befehle kann auch der Agent des Koordinators ausführen, wenn Sie ihn darum bitten. Dann ist er verpflichtet, Ihnen den Namen jeder Sitzung zu nennen. Danach läuft alles wie im Kapitel zu peeragent: Der erste Bildschirm endet meist mit der Vertrauensabfrage, und die Regeln dort gelten je Sitzung. Bei fünf Komponenten sind das fünf Sitzungen. Führen Sie also Buch, welche Sitzung zu welcher Komponente gehört.

![Wie zuvor. Die fünf Komponenten stehen jetzt in einem grauen Container mit dem orangen Reiter tmux und dem Zusatz: eine Sitzung je Agent. Die fünf Pfeile vom Koordinator zu den Komponenten sind orange, neben ihnen steht zusätzlich: peeragent startet. Der Koordinator liegt außerhalb des Containers.](bilder/H040-gesamtbild-2.svg)

**peeragent und tmux kommen dazu.** peeragent startet je Komponente einen Agenten, und jeder läuft in einer eigenen tmux-Sitzung weiter. Alle Pfeile führen nach unten: Ein Weg zurück besteht noch nicht.

Sechs Agenten laufen jetzt, jeder mit seinem eigenen Fenster. Die Sitzungen überleben den Aufruf von peeragent und eine getrennte Verbindung. Sie können jederzeit hineinsehen und dem Agenten dort schreiben, etwa wenn er beim Einrichten etwas von Ihnen wissen will.

Zwischen den Agenten besteht aber keine Verbindung. Das Bild zeigt es: peeragent hat seine Arbeit getan und ist weg. Nichts meldet sich von allein beim Koordinator.

## Schritt 3: simple-a2a und Wiki

Der Rückweg heißt im Regelwerk [Nachricht](../Z-anhang/Z010-glossar.md#nachricht). Alles, was ein Repo einem anderen mitteilt, ist eine: eine Lieferung, der Abschluss einer [Marke](../Z-anhang/Z010-glossar.md#marke), eine vereinbarte Schnittstelle, ein Befund, ein Änderungswunsch. Eine solche Nachricht ist eine Datei in `output/nachrichten/` des Absenders, mit Nummer, Absender, Empfängern, Datum, Art und dem, was sie erwartet: eine Buchung, eine Antwort oder nichts. Ab der Anlage ist sie eingefroren. Eine Korrektur ist eine neue Nachricht mit Verweis auf die alte.

Das Wort kennen Sie aus dem vorigen Kapitel in einem zweiten Sinn: der Text im Postfach. Beides passt zusammen. Die Datei ist die Nachricht, das Werkzeug stellt ihren unveränderten Inhalt zu. Format und Buchung sind bei jedem Transport gleich. Darum lässt sich der Transport wechseln, ohne dass sich an der Arbeitsweise etwas ändert.

Im Bild steht simple-a2a: ein Realm, darin ein Team `done`, je Agent ein Postfach. Es gilt der Maßstab aus dem Kapitel [simple-a2a](H030-simple-a2a.md). Laufen alle sechs Agenten bei Ihnen auf einem Rechner und unter einem Konto, genügt der Skill a2a, und im Bild ändert sich nur die Beschriftung des Bands. Der Dienst lohnt sich, wenn der Absender geprüft sein soll, wenn mehrere Rechner beteiligt sind oder wenn jemand von außen mitlesen soll.

Das Bild baut in der Reihenfolge des Verstehens auf. Beim echten Start ist die Reihenfolge eine andere: erst der Transport, dann die Einladung, zuletzt der Start, wie im vorigen Kapitel. Der Startprompt nennt die Wahl für den Transport, und der Agent der Komponente braucht seinen Zugang von Anfang an. Adresse und Einladung gehören bei simple-a2a in eine eigene Datei, nicht in den Prompt. Sie liegt wie jedes Geheimnis außerhalb der Repos, der Startprompt nennt nur ihren Pfad.

![Wie zuvor, tmux jetzt mit blauem Reiter und die Pfeile vom Koordinator schwarz. Der Koordinator und jede Komponente tragen unten einen orangen Streifen Wiki. Unter allem liegt ein breites oranges Band: simple-a2a, Postfächer und Rückweg. Von jeder Komponente und links am Container vorbei vom Koordinator führt ein Doppelpfeil zu diesem Band.](bilder/H040-gesamtbild-3.svg)

**simple-a2a und Wiki kommen dazu.** Jedes Projekt hat sein eigenes Wiki, und alle Agenten sind über simple-a2a verbunden. Jetzt gibt es den Rückweg: Nachrichten laufen in beide Richtungen, auch zwischen den Komponenten.

Das Wiki ist auch im Verbund die Quelle der Wahrheit, nur gibt es jetzt sechs davon. Wer eine Nachricht empfängt, bucht daraus in seine eigenen Register und vermerkt die Quelle. Ein Agent trägt nie etwas bei einem anderen ein. Beim Koordinator landen drei Dinge an festen Orten:

- Eine vereinbarte Schnittstelle kommt in das Verzeichnis der Schnittstellen, das der Koordinator führt. Das Regelwerk nennt sie Contract.
- Eine Lieferung und der Abschluss einer Marke werden als Zeile an der Marke gebucht.
- Ein Befund oder ein Änderungswunsch kommt in das passende Register, in dem solche Punkte gesammelt werden.

Für den Koordinator gilt dabei ein Leitsatz: Er bucht nur, was er für ein eigenes Freigabedokument oder seine Freigaben braucht. Alles andere liest er beim Nachbarn. Zwischenergebnisse, Entscheidungen, Spezifikationen, Testpläne und Fehlermeldungen der Komponenten gehören nicht in sein Wiki. So bleibt sein Wiki beim Ganzen.

Je Marke meldet jede Komponente zwei Dinge, jeweils mit der Erwartung einer Buchung: ihre Lieferung und den Abschluss ihrer Marke. Ist ihr Produkt seit dem Tag der Vormarke unverändert, entfällt eine neue Lieferung. Dann meldet sie die Übernahme mit dem Abschluss der Marke, und der Koordinator bucht den alten Tag.

Nachrichten erreichen nur einen laufenden Agenten. Einen Modus, der einen ruhenden Agenten weckt, gibt es nicht. Deshalb prüft der Agent jedes Projekts beim Sessionstart, täglich und bei jeder eingegangenen Nachricht, ob eigene Nachrichten noch ohne Quittung sind und ob an ihn gerichtete noch nicht gebucht sind. Das Regelwerk nennt diese Prüfung den Nachrichten-Wächter. Er meldet, er blockiert nicht.

## Beispiel DONE: ein Feld mehr

Der Agent der Mobile-App merkt, dass er zu jedem TODO ein weiteres Feld braucht. Die Schnittstelle gehört dem Backend, also dem Koordinator. Das Repo, das einen Gegenstand verantwortet, entscheidet über ihn; bei einer Schnittstelle ist das der Anbieter, im Regelwerk Provider.

Der Agent ändert das Backend also nicht selbst. Er legt in seinem eigenen `output/nachrichten/` eine Nachricht ab: Änderungswunsch an `done`, erwartet eine Buchung. simple-a2a stellt ihren Inhalt ins Postfach des Koordinators. Der Agent des Koordinators bucht den Wunsch in sein Register. Entschieden wird dort, innerhalb der freigegebenen Grundlagen. Im Streitfall entscheiden Sie.

Reicht die Änderung weiter und betrifft sie die Grundlagen des Koordinators, also Funktionsbeschreibung, Zuschnitt der Komponenten oder Übergabe, schickt er den betroffenen Komponenten einen Rücklauf. Die Freigabedokumente einer Komponente, die auf das alte Übergabe-Dokument verweisen, sind damit überholt.

Das Ganze wiederholt sich auch nach unten. Zerlegt eine Komponente selbst weiter, ist sie für ihre Teile Koordinator und bleibt nach oben Komponente.

## Wer was trägt

Am Ende hat jedes Werkzeug dieses Teils eine Aufgabe:

| Baustein | Aufgabe im Zusammenspiel |
|---|---|
| [Subagent](H010-subagenten.md) | erledigt in jedem Projekt kurze Schritte wie Recherche und Prüfung, damit das Fenster frei bleibt |
| [peeragent](H020-peeragent.md) | startet den Agenten einer Komponente und meldet den ersten Bildschirm |
| tmux | hält jeden Agenten am Laufen und lässt Sie hineinsehen |
| [simple-a2a oder skill-a2a](H030-simple-a2a.md) | stellt den Inhalt der Nachrichten zu |
| Wiki | hält in jedem Projekt das, was dort gilt |

Sie bleiben dabei die Stelle, an der alles zusammenläuft. Die Start-Tabelle, die Übernahme-Art und der Weg für Start und Transport liegen bei Ihnen, ebenso die Freigaben. Dass Agenten miteinander reden, spart Ihr Fenster, nicht Ihre Verantwortung.

## Was jetzt klar sein sollte

- Ein großes System wird zerlegt: Der Koordinator zerlegt und führt zusammen, jede Komponente ist ein eigenes Projekt mit eigenem Repo, Wiki und Agenten. Bei DONE ist jeder Zugang eine Komponente, das Backend bleibt beim Koordinator.
- Vor dem Start einer Komponente entscheiden Sie, mit Start-Tabelle, Übernahme-Art und dem Weg für Start und Transport. Die Komponente beginnt mit einem Startprompt und dem freigegebenen Übergabe-Dokument.
- peeragent startet die Agenten, tmux hält sie am Laufen, und simple-a2a oder skill-a2a bringt die Nachrichten. Beim echten Start kommt der Transport zuerst, denn der Startprompt nennt ihn.
- Jedes Repo schreibt nur sein eigener Agent. Mitgeteilt wird über Nachrichten, die als Datei beim Absender liegen. Der Empfänger bucht daraus in seine eigenen Register, der Koordinator nur, was er braucht.

Damit endet die Lesekette. Wenn Sie es selbst versuchen wollen, beginnen Sie mit dem Startprompt in [DONE mit Referenzprozess](../Y-beispiele/Y040-done-mit-referenzprozess.md).
