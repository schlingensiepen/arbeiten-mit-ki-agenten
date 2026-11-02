# DONE mit Referenzprozess

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `README.md`, `INIT.md`.

Dies ist der [Startprompt](../Z-anhang/Z010-glossar.md#startprompt) für das zweite Beispiel des Skripts, die Aufgabenverwaltung DONE. Anders als der Prompt zur [Lagerverwaltung](Y010-lagerverwaltung.md) erklärt er dem Agenten nicht, wie gearbeitet wird. Das übernimmt der [Referenzprozess](../Z-anhang/Z010-glossar.md#referenzprozess), eine öffentliche Vorlage mit Regelwerk und Anleitung. Der Prompt muss nur drei Dinge sagen: wo die Anleitung liegt, wie die Fragen beim Einrichten beantwortet sind, und worum es in dem Projekt geht. Das ist alles, was ein Regelwerk nicht wissen kann.

## Der Prompt

```text
Richte dieses Verzeichnis als neues Projekt nach der Anleitung unter https://github.com/schlingensiepen/referenzprozess-softwareentwicklung ein.

Meine Entscheidungen für das Einrichten:
- Einbindung: B, verknüpfte Vorlage. git init und das Kopieren der Projektdateien darfst du ausführen.
- Ein Repo, kein Remote.
- Kein WorkspaceManager.
- Bearbeiter-Kürzel: DON.
- Commit-Sprache: A, Projektsprache Deutsch.
- Prüfungen: Ein-Modell-Weg, falls du kein zweites Modell erreichst.
- Rolle: Koordinator.
- Erste Marke: 1.0, Erster Release.
- Keine Konzept-Sammlungen übernehmen, MADR nicht verwenden.
- Das Mission Statement leitest du aus dem Text unten ab, ich bestätige es dann.

Das Projekt: DONE ist eine Aufgabenverwaltung für mehrere Benutzer nach der Methode Getting Things Done. Der Name steht für Decide, Organize, Navigate, Execute, und er stellt das Ziel in den Mittelpunkt, nicht die offene Arbeit.

Das System besteht aus einem Backend mit WebAPI und mehreren Zugängen darauf: Mobile-App als PWA, Desktop-App als Webanwendung, Kommandozeilen-Werkzeug, MCP-Server für Agenten und ein Messenger-Bot, der aus jeder Nachricht ein TODO macht.

Fachlicher Kern:
- TODOs haben Sub-TODOs und Abhängigkeiten. Daraus berechnet das System Deadlines und die Sicht „Kann sofort erledigt werden“.
- Tags lösen die Kategorien der Methode ab. Was keinen Tag hat, liegt in der Inbox.
- Gespeicherte Sichten filtern nach Tags, Terminen und Text und können Untersichten haben.
- TODOs lassen sich an andere Benutzer delegieren. Beide Seiten behalten ein eigenes, verlinktes TODO.

Was beim Einrichten noch offen ist, frag mich gesammelt in einem Block. An vielen Stellen bin ich oberflächlich geblieben. Was du fachlich nicht verstehst oder nur mit Annahmen umsetzen kannst, frag mich nach dem Einrichten.
```

## Was er enthält

**Der erste Satz** ist der Start-Satz aus der README des Referenzprozesses, Wort für Wort. Er sagt dem Agenten, dass ein neues Projekt entstehen soll und wo die Anleitung dafür liegt. Der Agent liest sie direkt von dieser Adresse, bevor im Ordner irgendetwas liegt. Mehr braucht es laut README nicht; alles Weitere fragt der Agent dann nach.

**Die Entscheidungen für das Einrichten** nehmen diese Fragen vorweg. Die Anleitung des Referenzprozesses, die Datei `INIT.md`, sieht beim Einrichten einen Fragen-Block vor: Wie kommt die Vorlage ins Projekt, ein Repo oder zwei, welches Kürzel, welche Sprache für Commits, wie wird geprüft, welche Rolle hat das Projekt, wie heißt die erste Marke, und was ist der Auftrag. Dazu kommen Angebote, die der Agent beim Einrichten sonst macht: die Skripte laufen zu lassen, Konzept-Sammlungen zu übernehmen, ein Format für Architektur-Entscheidungen zu benutzen. Jede Zeile des Prompts beantwortet einen dieser Punkte, bevor er gestellt wird. Was die einzelnen Antworten bedeuten und warum man sie zu Beginn so wählt, erklärt [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md) Punkt für Punkt. Für den ersten Durchlauf genügt: Die Antworten sind die einfachsten, die der Referenzprozess zulässt. Ein Repo, kein Remote, kein zusätzliches Programm, nichts Optionales.

**Das Projekt** ist der Teil, den nur ein Mensch schreiben kann. DONE ordnet Aufgaben nach [Getting Things Done](../Z-anhang/Z010-glossar.md#getting-things-done), einer Methode, die Aufgaben aus dem Kopf in ein verlässliches System holt. Der Absatz zu den Bestandteilen nennt, woraus das System besteht: ein [Backend](../Z-anhang/Z010-glossar.md#backend), der Teil, der im Hintergrund auf einem zentralen Rechner läuft und die Daten hält, mit einer [WebAPI](../Z-anhang/Z010-glossar.md#webapi), einer Schnittstelle, über die Programme den Dienst über das Netz ansprechen. Darauf setzen die Zugänge: eine [PWA](../Z-anhang/Z010-glossar.md#pwa), ein Programm, das im Browser läuft und sich wie eine App auf dem Telefon installieren lässt; eine Webanwendung für den Schreibtisch; ein Kommandozeilen-Werkzeug für das [Terminal](../Z-anhang/Z010-glossar.md#terminal); ein [MCP-Server](../Z-anhang/Z010-glossar.md#mcp-server), der einem Agenten die Funktionen des Systems als Tools anbietet; und ein Bot, der in einem Messenger aus jeder Nachricht eine Aufgabe macht. Der fachliche Kern darunter nennt in vier Punkten, was DONE von einer gewöhnlichen Aufgabenliste unterscheidet.

**Der letzte Absatz** regelt die Fragen. Was beim Einrichten offen bleibt, soll der Agent gesammelt stellen, nicht eine nach der anderen. Die fachlichen Fragen kommen danach. Der Prompt sagt offen, dass er an vielen Stellen oberflächlich ist, und macht daraus einen Auftrag: nachfragen statt annehmen.

## Wie Sie ihn benutzen

Legen Sie einen leeren Ordner an und starten Sie darin Ihren Agenten. Sie brauchen dabei Internet, weil der Agent die Anleitung und die Vorlage von GitHub holt. Fügen Sie den Prompt als erste Nachricht ein. Im Terminal ist vorher nichts weiter zu tun.

Der Agent liest die Anleitung, bindet die Vorlage ein, kopiert die Projektdateien und legt den ersten Commit an. Die Anleitung verlangt für das Einbinden und Kopieren Ihre Zustimmung; die zweite Zeile des Prompts gibt sie vorab. Danach legt er Ihnen vor, was noch offen ist, und bildet aus dem Text den Entwurf des Mission Statements, einer kurzen Beschreibung, was das Projekt ist und für wen. Den bestätigen Sie oder ändern ihn. Erst dann kommen die fachlichen Fragen.

Eine frühere Fassung dieses Prompts ist mit dem Referenzprozess durchgespielt worden. Das Projekt stand nach wenigen Minuten, ohne dass der Agent irgendwo hängen blieb. Die Punkte, die er dabei noch nachfragte, sind seither in den Prompt aufgenommen. Rechnen Sie trotzdem mit Rückfragen: Die Vorlage entwickelt sich weiter, und der Agent fragt lieber einmal zu viel.

Wenn Sie den Prompt für ein eigenes Projekt nehmen, ändern Sie zwei Dinge: das [Bearbeiter-Kürzel](../Z-anhang/Z010-glossar.md#bearbeiter-kürzel), drei Buchstaben, die zeigen, wer eine Datei bearbeitet hat, hier `DON` für DONE, und alles ab „Das Projekt“. Die Entscheidungen für das Einrichten lassen Sie beim ersten Mal, wie sie sind.

## Was jetzt klar sein sollte

- Ein Startprompt mit Referenzprozess hat drei Teile: den Start-Satz, die Antworten auf die Fragen des Einrichtens, und das Projekt.
- Wie gearbeitet wird, steht nicht im Prompt. Das holt sich der Agent aus der Anleitung.
- Der Teil, den nur Sie schreiben können, ist das Projekt. Dort darf der Prompt lückenhaft sein, wenn er dem Agenten sagt, dass er fragen soll.

Was derselbe Auftrag kostet, wenn man dem Agenten alles selbst erklärt, zeigt [DONE ohne Regelwerk](Y030-done-ohne-regelwerk.md). Wie der Agent mit diesem Prompt das Projekt aufsetzt, zeigt Schritt für Schritt [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md).
