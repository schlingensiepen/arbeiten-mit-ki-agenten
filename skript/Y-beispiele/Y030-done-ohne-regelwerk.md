# DONE ohne Regelwerk

> **Stand der Quellen:** keine gebundene Quelle. Der Prompt ist das Original, mit dem das Beispiel DONE begonnen hat, um einen Vornamen, einen lokalen Pfad und ein internes Werkzeug bereinigt.

**Dieses Kapitel ist zum Lesen da, nicht zum Benutzen.** Wer DONE selbst aufsetzen will, nimmt den Prompt aus [DONE mit Referenzprozess](Y040-done-mit-referenzprozess.md). Der Prompt hier ist derselbe Auftrag ohne diesen kurzen Weg: der [Startprompt](../Z-anhang/Z010-glossar.md#startprompt), mit dem das Projekt DONE tatsächlich begonnen hat, in voller Länge. Er steht im Skript als Beleg. Er zeigt, was es kostet, einem [Agenten](../Z-anhang/Z010-glossar.md#agent) die ganze Arbeitsweise selbst zu erklären, und zwar in jedem Projekt von Neuem.

## Was er zeigt

Lesen Sie den Prompt nicht Zeile für Zeile. Überfliegen Sie ihn und achten Sie auf drei Dinge.

**Erstens die Länge.** Rund dreihundert Zeilen, in einem Stück, als erste Nachricht an den Agenten. Der kurze Prompt kommt mit fünfzehn Zeilen aus und richtet dasselbe Projekt ein.

**Zweitens die Mischung.** Fachliches und Vorgehen wechseln sich ab, ohne Ordnung. Zwischen den Bestandteilen des Systems und den Regeln für Aufgaben, Tags und Sichten steht, wer wann prüft, wie Fragen zu stellen sind, wie weitere Agenten angelegt und benannt werden, wer einen Vertrag zwischen zwei Komponenten verantwortet, wie ein Testplan aufgebaut ist und welche Dokumente für Benutzer entstehen. All das ist Arbeitsweise. Nichts davon ist DONE. In [DONE mit Referenzprozess](Y040-done-mit-referenzprozess.md) fehlt dieser Teil vollständig, weil das Regelwerk ihn übernimmt. Was dort bleibt, das Projekt und sein fachlicher Kern, steckt auch hier drin, nur verteilt auf das Ganze.

**Drittens die Haltbarkeit.** Der Prompt nennt Werkzeuge und Modelle beim Namen: ein Werkzeug für Recherchen, eines für Oberflächen, eines für die Prüfung von Code, dazu den Namen eines Modells. Er setzt Dinge voraus, die nur auf dem Rechner seines Verfassers so vorhanden waren. Ein solcher Prompt stimmt genau einmal. Beim nächsten Projekt haben sich die Werkzeuge geändert, und der Text muss neu geschrieben werden.

Eine Prüfung dieses Prompts gegen das Regelwerk des Referenzprozesses hat ergeben, was man nach dem Überfliegen erwartet: Vieles, was er regelt, regelt das Regelwerk schon, und an mehreren Stellen anders. Wertvoll ist der fachliche Teil. Die Mechanik kann ein Regelwerk übernehmen, und genau das tut der kurze Prompt.

Drei Hinweise zum Lesen. Der Prompt nennt in der vierten Zeile eine Regelwerks-Datei, erklärt das Vorgehen danach aber trotzdem vollständig selbst; das ist der Punkt, nicht ein Versehen. Er duzt den Agenten, wie die meisten Prompts das tun. Und er hat Tippfehler und lose Enden, weil er so abgeschickt wurde. Gegenüber dem Original sind drei Stellen geändert: Ein Vorname ist durch eine neutrale Formulierung ersetzt, ein Pfad auf dem Rechner des Verfassers ist entfernt, und ein Werkzeug, das es nur dort gab, ist durch eine Umschreibung ersetzt. Sonst ist der Text, wie er war.

## Der Prompt

```text
Wir implementieren eine TODO-Liste nach dem Pattern, "getting things done".
https://de.wikipedia.org/wiki/Getting_Things_Done

Bitte lies MasterPrompt.md und arbeite das ab, lege unser Projekt so an, dass ein
Software-System entwickelt werden kann. Ich stelle Dir hier schon mal das Projekt vor,
ich denke zum Aufsetzen des Projektes wirst Du noch Fragen haben, bitte dann einfach
stellen, wenn sie auftauchen.

Zur Methode "getting things done" machen wir über NotebookLM eine deep recherche und lassen uns die
grundlegende Methode erklären. Am besten gleich starten, so eine Recherche dauert etwas.

Im folgenden erkläre ich Dir jetzt meine Ideen zur App und das erste was wir machen, wenn das
Projekt eingerichtet ist, wir gehen gemeinsam die Abweichungen
zur Methode durch, so dass ich festlegen kann, was im Einzelfall gilt.

Wir haben uns für den Namen DONE entschieden.

Der wesentliche Grund ist, dass wir nicht das Problem, sondern das Ziel in den Mittelpunkt stellen.
Die meisten Aufgabenverwaltungen fokussieren auf offene Aufgaben, ToDos und unerledigte Arbeit.
Unser Ansatz orientiert sich dagegen am gewünschten Zustand: Dinge sollen zuverlässig erledigt werden.

DONE steht dabei für:

Decide
Organize
Navigate
Execute

Der Name beschreibt den Weg von einer neuen Aufgabe bis zu ihrer Erledigung und verkörpert gleichzeitig
das Ergebnis, das Nutzer erreichen möchten: done.

Im Vergleich zu Alternativen wie CORE wirkt DONE als Produktname unmittelbarer, verständlicher und motivierender.
Nutzer wollen keine Aufgaben verwalten, sie wollen, dass Aufgaben erledigt sind. Genau diese Perspektive soll unser Produkt widerspiegeln.

Daher verwenden wir den Projektnamen: DONE.

Das ganze soll aus Teilen bestehen,
- einem Backend mit einer WebAPI
- einer Mobile-App (als PWA)
- Desktop-App (als Webanwendung)
- Einem Bot, der über einen Messenger erreichbar ist und aus jeder Message einfach direkt ein TODO erzeugt.
- Einem Worker, der ein EMAil-Postfach überwacht und eingehende Mails in TODOs umwandelt
- einem lokalen MCP-Server
- einem MCP-Server via streamable http
- einem cli-tool
- einem Skill, der erklärt, wie ein Agent die WebAPI verwendet
- einem Skill, der erklärt, wie ein Agent man das cli-Tool verwendet

Beim Aufsetzen wählen wir dazu den Referenzprozess zur Software-Systementwicklung, der auch
vorsieht, dass es neben uns, weitere Peer-Agenten gibt. Wir sammeln hier in unseren wiki die
Single Source of Truth, die anderen können die gerne lesen, wenn sie was geändert haben wollen
sollen sie eine Nachricht schicken und wir zwei besprechen die dann, bevor Du diese aufnimmst.
Das ganze ist aber ohnehin im Referenzprozess beschrieben.
Wir sind also für die Anforderungen und die Systemspezifikation zuständig.

Schlage für die anderen sinnvolle Namen vor und zeige mir die, bevor Du startest, ich hatte mir das grob schematisch so vorgestellt:
done-backend: Verantwortet das Backend
done-mobile: Verantwortet die Mobile-App
done-web: Verantwortet die Desktop-App
done-mcp: Ein MCP-Server, der als Client gegen das Backend arbeiten kann, dass ich die Funktionen der App auch innerhalb einer Agenten-Session nutzen kann.

sie liegen jeweils in gleichnamigen Nachbarverzeichnissen (also z.B. ../done-backend)

Für die Anlage von Peer-Agenten beschaffe Dir die Informationen über das
dafür vorgesehene Werkzeug und lasse mich entscheiden, mit welchen Templates die Agenten erstellt werden.

Das Vorgehen ist wie folgt: Wir spezifizieren hier erst mal das Gesamtsystem.
Um das tun zu können, sammeln wir alle Anforderungen an das System.
Und pflegen das in unser lokale wiki ein.

Mit dem im Prozess vorgesehenen Glossar stellen wir sicher, das Begriffe in allen Kontexten von allen Agenten gleich verwendet werden.
Der Glossareintrag ist dabei mehr als ein
klassischer Glossareintrag mehr eine Art Lexikoneintrag.

Wenn die Anforderungen gesammelt sind, lassen wir einen Fable Sub-Agenten Konsistenz prüfen dabei soll
er die Anforderungen untereinander und auch die Begriffe gegen das Glossar prüfen und er soll prüfen ob es
Definitionslücken gibt, die eine sauber Spezifikation des Systems erschweren, denn dann legen wir erstmal
diese fest, bevor wir weitermachen.

Dann besprechen wir notwendige Änderungen und da machen wir so lange, bis alles konsistent ist.

Dann spezifizieren wir das Gesamtsystem, dann legen wir die Architektur fest und schneiden damit die Subsysteme und
legen für jedes einen Peer-Agent an (s.o.)

Wenn das durch ist, machen wir noch mal eine Runde Konsistenzprüfung der Spezifikation durch Fable.


Bevor die Peer-Agenten dann Teilsystemspezifikationen schreiben können, müssen Sie zusätzliche Anforderungen abfragen und klären.
Dazu müssen Sie festlegen, welche Komponente mit einer anderen einen Contract hat.
Welche Art von Contract es ist, also API-Zugriff oder gesharter Code oder gesharte Datenbank oder Ähnliches
Und wer den Contract verantwortet, zur Ordnung der Verantwortlichkeit wird dann vom Anwender freigegeben.
Es gilt als Regel: Der Verantwortliche ist auch für die Implementierung zuständig, und alle Änderungswünsche am Contract
werden ihm als Nachricht vorgetragen. Er alleine entscheidet zusammen mit den Anwender über Änderungen am Contract.

Die Peeragenten legen dann Teilsystemspezifikationen an, dann lassen wir je einen Faible-Agenten die Teilspezifikationen gegen die SSOT validieren.

Jeder Agent, der etwas verantwortet und eine Benutzungs-Schnittstelle hat,
nutzt dazu das Stitch-Plugin. Immer wenn der Anwender meint, er habe jetzt eine ausreichende Menge an Screens erzeugt, lassen wir
einen Faible-Agenten laufen, der prüfen soll, ob alle Fälle aus der Spezifikation abgebildet sind.

Wird dabei die Spezifikation angepasst, wird auch ein weiterer Faible-Lauf zur Prüfung gegen SSOT fällig.

Wenn das durch ist, geht es an die Implementierung. Jeder Agent entscheidet ob er das selber macht oder ob er dazu einen Subagenten beauftragt.
Wenn dazu legt er in seinem Unterverzeichnis die üblichen zur gewählten Technologie passenden Unterverzeichnisse (Konventionen beachten, bei nicht eindeutig, fragen, welche Konvention beachtet werden soll, wenn unsere Projektspezifikation mit
der Konvention inkompatibel ist, wenden wir die Spezifikation auf der src-Verzeichnis an.)

Wenn wir damit durch sind, lassen wir über das codex-Plugin einen Codereview über die Implementierung laufen und setzen dann in
Rücksprache mit den Anwender die Anregungen um.


Für unsere App stelle ich mir Folgendes vor:

Das Ganze soll eine Multi-User-Anwendung werden. Es muss also die Möglichkeit geben, dass ich jemand anderem ein
To-do vorschlage und er es dann entsprechend seinen Vorstellungen in die eigene Liste übernimmt.

Außerdem sollen unsere To-do's aus Sub-to-do's bestehen können. Es gibt dann auch für To Do's geschätzte Dauer, eine festgelegte
und eine berechnete Deadline.
Deshalb haben die To-Dos auch die Möglichkeit, zu definieren, was abgearbeitet sein muss, bevor sie bearbeitet werden können.
Dazu ist es also auch notwendig, eine GUI zur Verfügung zu stellen, indem ich in einem To-do die Sub-To-Dos sortieren kann.
Das will der Anwender ja nicht von Hand da reinfummeln müssen. Das System soll also dann immer die Deadlines neu berechnen,
wenn sich hier Abhängigkeiten ändern.

Es gibt also neben der direkten Abhängigkeit auch die implizite Abhängigkeit, ein TODO trägt dazu ein Flag, ob seine sub-TODOs unabhängig sind
oder ob deren geordnete Abarbeitung einen Abhängigkeitsreihe beschreibt.

Wir definieren analog in Kontexten aus der Basismethode Tags. Diese Tags dienen zum Filtern der Ansichten, daher sollen Sie
auch noch weitere Eigenschaften haben, z.B. einen Link auf einen anderen User, der für die Bearbeitung notwendig ist, und
einen Ort, so dass man abhängig vom Standort des Telefons filtern kann "z.B. alles was getaggt ist mit 3km Umkreis von hier"

Es gibt TAGs, die einfach nur eine von 16 Standardfarben repräsentieren, wenn die vergeben sind, werden Elemente, die ein TODO
darstellen in dieser Farbe dargestellt, die Farb-Tags sind daher nur einmal zu pro TODO zu vergeben, d.h. eine neue Zuweisung
überschreibt die aktuelle "Farbe".

Es gibt globale Tags und Tags nur für User, wir ein TODO delegiert, werden globale Tags an die anhängige Kopie übertragen
und dort auch aktuelle gehalten.

Suchfilter müssen aus verschiedenen Suchkriterien zusammengebaut werden können und als Sichten abgespeichert werden können.
Sichten soll Untersichten enthalten, die jeweils den Filter verfeinern
z.B. "Alles was ich delegiert habe" mit den Unterpunkten "Alles was ich an eine bestimmte Person delegiert habe." usw.

Dann müssen wir mal eine Liste von Standardsichten definieren, die das System automatisch bereitstellt.

Als Regel für eine GUI gilt immer, wenn ich irgendwo suche oder auf To-dos zugreifen möchte.
Als Dropdown eine Liste aller Ansichten angeboten und durch einen Texteingabe, die als weiterer Textfilter wirkt, ergänzt.

Es soll möglich sein TODOs mit einer Delegationsnachricht zu delegieren,
dann tauchen diese in der Inbox des anderen auf, und bleiben als delegiert in der
eigenen Liste enthalten, wird der delegierte TODO als erledigt gekennzeichnet, schaltet der delegierende wieder auf "offen"
enthält im Feld "Delegierungsstatus", die Information, dass der andere am ... abgeschlossen hat. Und im Feld
Delegationsantwort die Antwort des Bearbeiters.

Jedes TODO hat einen Changelog, in dem eigene Änderungen und auch Änderungen am Bearbeitungsstand und Delegation vermerkt sind.
Wichtig: Das delegierte TODO und das delegierende TODO sind in diesem Sinne eigenständige TODO, die lediglich verlinkt sind,
ein TODO kann mehrfach an verschiedene andere delegiert werden


Da ein To-do, auch von mehreren anderen TODO abhängen kann, gibt es in der Desktop-App noch einen Abhängigkeitsgraph für
kompliziertere Fälle dieser enthält eine Liste mit TODOs (entsprechend des Standardzugriff auf TODO mit Ansichten und Textfilter) und einen Canvas,
TODO können aus der Liste in den Canvas per Drag-n-Drop übertragen werden. Als Regel gilt, zwischen den sichtbaren TODO werden
Abhängigkeiten als Pfeil dargestellt. TODO, die unsichtbare Abhängigkeiten haben, werden anders dargestellt und haben ein Kontext-Menü
"expandieren", das die anhängigen und die voraussetzenden in den Cavas bring. Löschen eines TODO im Canvas löscht nur seine Ansicht, nicht das Element.
Der Standard-Screen zur Bearbeitung eines TODO wird eingeblendet und zeigt immer das gerade aktive TODO zur Bearbeitung an.
Mehrfachauswahl für Löschen, Bewegen, etc. ist möglich.
Es gibt eine Funktion "verbinden", die alle Pfade zwischen den ausgewählten Elementen in den Canvas bringt.
Es gibt zwei Versionen full expand, die eine Expandiert ausgehend von der Auswahl in Richtung der Anhängigkeit, die andere in die andere Richtung. Jeweils bis zum Ende.

Kritischer Pfad, es gibt eine Ansicht "kritischer Pfad", der mögliche kritische Pfade anzeigt, da müssen wir aber noch mal besprechen wie das genau aussehen soll.

Bevor Du einen Plan ausarbeitest, stelle mir erstmal die offenen Fragen zum Vorgehen, wenn die geklärt sind, erstelle den Plan
und fange dann an mir offene Fragen zur Funktion zu stellen.
Wichtig: Immer jede Frage einzeln und mit kurzem Kontext-Briefing und wir fangen immer mit den
Fragen an, die am meisten Vorfestlegungen verursachen, so dass sich ggf. andere Fragen erübrigen.

Wenn ich es richtig verstehe, dann sind in der Ursprünglichen Methode die TODOs, wenn die reinkommen in einer INBOX, weil sie
von da Kategorien zugeordnet werden müssen, die TAGs lösen bei uns ja die Kategorien ab, daher ist
alles, was keinen Tag hat in der Inbox.

Wenn nur eines der Farbtags zugeordnet ist, dann wäre das ja über eine Ansicht filterbar (Alles was nur gelb hat und nichts anderes.)
wir bieten aber schon vorgefertigte Ansichten an (Inbox (gelb), Inbox (rot) ...) die werden natürlich dann auch gleich
farblich markiert dargestellt.

TODOs haben eine Art "Betreff", das ist nur ein String, sie haben aber auch eine Langbeschreibung, da müssten wir mal abwägen, ob das
ein Subset von HTML oder MD oder beide sein kann (dazu müssten wir ein Subset von HTML definieren, das wirklich komplett nach MD
und von MD abbildbar ist. Am besten machen wir dazu noch eine Recherche, die uns dann auch gleich Sanitizer mir recherchiert.

Was auch nicht blöd wäre, wenn man die Beschreibung nicht nur direkt als Parameter, sondern auch als Parameter, der einen Dateinamen
enthält übergeben könnte. In letzterem Fall würde der Inhalt der Datei übernommen. Das wäre für den MCP und den CLI sicher gut, wahrscheinlich braucht
man dafür an der API so etwas, wie ein upload_large_text und da bekommt man denn eine GUID und die passt man in die anderen
Schnittstellen, besonders spannend wird das bei der Änderung eines Textes an einem TODO, aber da wir die ja sowieso einem Tracker unterwerfen
gibt es dann einfach einen neuen Upload und der Update-Call bekommt die GUID mit dem neuen Text.

Aus der Möglichkeit TODOs untereinander abhängig zu machen folgt, dass es eine Sicht geben kann "Kann sofort erledigt werden."

Alle unsere Standardsichten, also die, die das Programm schon eingebaut hat, sollen so modelliert sein, wie die vom Anwender angelegten Sichten,
so dass man mit COPY eine eigene editierbar Sicht daraus erstellen kann.

Der Sichten-Editor wird ein Kernstück über seine Funktion müssen wir noch ausgiebig sprechen.

Jedes TODO soll die Möglichkeit habe, Dateien mit Namen anzuhängen. In den GUI soll das mit den plattform-typischen
Benutzungsmethoden gehen, also Drag'n'Drop auf dem Desktop und die üblichen "Aus Galerie, ... einfügen"-Funktionen
in der mobile-Version.

Ein TODO muss auch eine geschätzte Dauer haben, sonst klappt das mit der Abschätzung der Dringlichkeit nicht.

Jedes TODO hat mehrere Datumsfelder: Deadline, deferred_to (wird erst dann wieder angezeigt, es sei denn die View legt das anders fest),
planned_at (eine Zeitspanne in der das geplannt ist, daraus folgen auch neue Filterkriterien, "was ist gerade geplant bzw. war schon geplant",
"was ist xxx (morgen / am 22.03.2027 / übermorgen / nächste Woche) geplant"

Dann brauchen wir noch einen TODO-Generator, der verschiedene Zeittrigger kennt
(täglich, montags, dienstags (also wöchentlich), monatlich (am x-ten eines Monats)
alle auch jeweils mit Uhrzeit. Der generator kennt relative Zeitangaben, so dass z.B.
montags um 8:00 ein TODO mit der Deadline kommender Freitag 18:00 und einem geplanten Bearbeitungsfenster mittwoch zwichen 13:00 und 14:00
erzeugt werden kann. Arbeite mal die Triggerarten und die sinncollen relativen Zeitangaben
als Liste aus und lege mir diese vor.

Wir erstelle einen Testplan für die Test, die nur ein Mensch durchführen kann, die MD-Version davon ist der Master für das
durchführen eines Text erstelle dann bitte eine Excelarbeitsmappe in dem der komplette Plan zum Abarbeiten hinterlegt ist,
dieses Excel-Dokument ist also die Instanz eines Testdurchganges.
Zeige mir vor dem Anlegen Deine geplante Struktur. Dieses Dokument dient dazu den
Testplan komplett zu beschreiben und gleichzeitig die Abarbeitung und die Ergebnisse
zu dokumentieren. Ich halte nichts davon, das in zwei Dokumente zu unterteilen.
Das Ding soll so aufgebaut sein, dass wir durch Wiedereinlesen des Dokumentes die
Rückmeldung des Testers gleich erfassen können.
Zielgruppe für den Testplan ist ein technisch unerfahrener Abiturient, wenn also technische Vorbereitungen zu
erledigen sind, müssten dafür auch Dokumentationen erstellt werden.

Zur Begleitung des Test nutzen wir NotebookLM zur Erstellung der Dokumentation für den User:

Dazu legen wir ein NotebookLM an, das startet mit einer Recherche zu den technischen Grundlagen

Da laden wir auch auch den Testplan und die Beschreibung unserer Software hoch, dann lassen wir NotebookLM jeweils einen:
- Erläuterung als Report
- einen Videoverview
- einen Audiooverview (brief)
- einen Audiooverview (deep dive, Podcasts)
- ein Slidedeck

zu den einzelnen Hintergrundthemen, den einzelnen Schritten zur Vorbereitung, der Vorstellung des Testplanes und zu den
einzelnen Testabschnitten erstellen.
Überlege erstmal mit mir, was für Dokumente wir dazu ins NotebookLM
laden müssten und welche davon dazu erst noch erstellt werden müssen.
Und schlage vor, zu welchen Themen Hintergrundrecherchen angestoßen werden sollen.
Ich würde diese gerne freigeben, bevor Du das Notebook anlegst.

Nach dieser Freigabe, startest Du bitte als Hintergrundtask die Recherchen und erstellst parallel die fehlenden Dokumente,
wenn die Recherche durch ist, löscht Du alle fehlgeschlagenen Quellen (Notebook hat gerne mal tote Links in der Recherche Liste)
und dann machst Du eine Sichtprüfung, ob die übrigen Quellen zur Themenstellung passen.

Und wenn das geschehen ist, lädst du die notwendigen Dokumente mit dem Prefix "Projekt - " ins Notebook. Denn nur so können wir
die von den recherchierten Quellen unterscheiden.

Dann überführen wir den Plan für die Artefakte in eine eigene Datei und ich gebe den Plan frei, das Ziel ist es dann
in einem Hintergrundtask das Erstellen der Artefakte zeitversetzt zu starten, so dass kein Ratelimit zuschlägt, ggf. müssen beim Fehlschlag
weitere Wartezeiten und Retry eingeführt werden.

Bitte beachte, dass bei NotebookML für das Erstellen von Artefakten die Quellen auf denen das Artefakt basiert vorgegeben werden können
das sollten wir auch machen, weil sonst unseres Funktionen und Hintergrundfunktionen gemischt werden.

Bevor Du etwas in Auftrag gibst, hätte ich gerne die konkrete Auftragsliste, zur Freigabe vorgelegt.

Analog zum Vorgehen zur Erstellung der Unterlagen zum Testplan gehen wir dann bei der Erstellung des Nutzerhandbuchs vor, Du
erstellst eine MD-Datei und wir überlegen, was wir noch brauchen und dann machen wir Recherche und Erstellung der Unterlagen für Endbenutzer
mit dem gleichen Vorgehen per NotebookLM, hier sind dann die Themen so zu wählen, dass es neben einer Gesamtübersicht auch
Artefakte zu bestimmten Aspekten oder Teilkapiteln gibt.

An ein TODO können auch Dateien angehängt werden.

Alle Schnittstellen sollten für alle Daten jeweils die Zeitzone
beinhalten, es muss eine Methode erarbeitet werden, wie man
zwischen der lokalen Zeit des Anwenders und der globalen Zeit
gemappt wird.

An den Benutzungsoberflächen soll es möglich sein ein TODO als
Folge-TODO anzulegen, also das aktuelle TODO als erledigt zu
markieren, aber eines oder mehrere neue "folgende" TODO zu erzeugen
(letzteres wäre dann ein Splitt), dazu bedarf es dann eine neuen
Verknüpfung zwischen TODOs, den auch die Rechte-Kette auflösen
können muss, bei einem TODO, dass auf einem anderen beruht, aber delegiert
wird, muss der Empfänger natürlich auch das zugrundeliegende abrufen können.
Beim Splitt soll es gleich möglich sein einzelne TODOs zu delegieren.
Beim Splitt muss es auch möglich sein, die Abhängigkeiten zu definieren:
Z.B. TODO A wird augesplittet in TODO B und TODO C, wobei B direkt an User X delegiert wird, C aber erst angefangen werden kann, wenn B fertig ist.

Wir implementieren Web-Anwendungen, wenn es geht nach dem Muster, dass eine zentrale
statische HTML-Datei komplett ohne Daten ohne Authentifizierung abrufbar ist, diese enthält Referenzen auf relativ
liegende CSS, JavaScript und sonstige Assets und einen Link zu einer API, aus der sich dann
das DOM hydriert, lies dazu mal
<Pfad zu einem API-Konzept aus einem früheren Projekt, hier entfernt>
und lass mich wissen, ob Du dazu noch Rückfragen hast.

Leite aus diesen Vorüberlegungen mal User-Stories, Use-Cases und Requirements ab, an vielen Stellen bin
ich oberflächlich geblieben, alles, was Du nicht verstehst oder nur mit Annahmen umsetzen kannst bitte als
Rückfrage formulieren. Ich hätte gerne jede Frage einzeln mit einem kurzen Briefing und Handlungsempfehlungen,
die gegeneinander abgewogen sind.
```

## Was jetzt klar sein sollte

- Ohne Regelwerk steht die Arbeitsweise im Prompt. Sie ist lang, vermischt sich mit dem Fachlichen und muss in jedem Projekt neu geschrieben werden.
- Der Teil, den nur der Mensch beisteuern kann, ist das Fachliche. Er ist in beiden Fassungen derselbe.
- Der Rest ist Mechanik. Sie gehört in ein Regelwerk, das der Agent liest, nicht in jeden Prompt.

Warum der naive Ansatz an diesem Aufwand und an anderem scheitert, begründet [Warum der naive Ansatz scheitert](../C-der-langfristige-ansatz/C010-warum-der-naive-ansatz-scheitert.md). Den Vergleich der beiden Prompts beim Aufsetzen zieht [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md).
