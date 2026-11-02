# DONE mit Referenzprozess

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `README.md`, `INIT.md`, `wiki/Konzept-Repositories.md`.

Dies ist der [Startprompt](../Z-anhang/Z010-glossar.md#startprompt) für das zweite Beispiel des Skripts, die Aufgabenverwaltung DONE. Anders als der Prompt zur [Lagerverwaltung](Y010-lagerverwaltung.md) erklärt er dem Agenten nicht, wie gearbeitet wird. Das übernimmt der [Referenzprozess](../Z-anhang/Z010-glossar.md#referenzprozess), eine öffentliche Vorlage mit Regelwerk und Anleitung. Der Prompt muss nur drei Dinge sagen: wo die Anleitung liegt, was der Agent ausführen darf und worum es in dem Projekt geht. Das ist alles, was ein Regelwerk nicht wissen kann.

## Der Prompt

```text
Richte dieses Verzeichnis als neues Projekt nach der Anleitung unter https://github.com/schlingensiepen/referenzprozess-softwareentwicklung ein.

git init, das Einbinden der Vorlage und das Kopieren der Projektdateien darfst du ausführen, jeweils auf dem Weg, den du empfiehlst.

Das Projekt: DONE ist eine Aufgabenverwaltung für mehrere Benutzer nach der Methode Getting Things Done. Der Name steht für Decide, Organize, Navigate, Execute, und er stellt das Ziel in den Mittelpunkt, nicht die offene Arbeit.

Das System besteht aus einem Backend mit WebAPI und mehreren Zugängen darauf: Mobile-App als PWA, Desktop-App als Webanwendung, Kommandozeilen-Werkzeug, MCP-Server für Agenten und ein Messenger-Bot, der aus jeder Nachricht ein TODO macht. Jeder Zugang soll später ein eigenes Projekt werden, dieses Projekt ist der Koordinator.

Fachlicher Kern:
- TODOs haben Sub-TODOs und Abhängigkeiten. Daraus berechnet das System Deadlines und die Sicht „Kann sofort erledigt werden“.
- Tags lösen die Kategorien der Methode ab. Was keinen Tag hat, liegt in der Inbox.
- Gespeicherte Sichten filtern nach Tags, Terminen und Text und können Untersichten haben.
- TODOs lassen sich an andere Benutzer delegieren. Beide Seiten behalten ein eigenes, verlinktes TODO.

An vielen Stellen bin ich oberflächlich geblieben. Was du fachlich nicht verstehst oder nur mit Annahmen umsetzen kannst, frag mich nach dem Einrichten.
```

## Was er enthält

**Der Startsatz** ist der Satz aus der README des Referenzprozesses, Wort für Wort. Er sagt dem Agenten, dass ein neues Projekt entstehen soll und wo die Anleitung dafür liegt. Der Agent liest sie direkt von dieser Adresse, bevor im Ordner irgendetwas liegt.

**Die Erlaubnis** ist der zweite Absatz. Die Anleitung, die Datei `INIT.md`, erlaubt dem Agenten `git init`, das Einbinden der Vorlage und das Kopieren der Projektdateien nur nach Ihrer Zustimmung. Der Absatz gibt sie vorab. Er legt keinen Weg fest, sondern überlässt dem Agenten den Weg, den er empfiehlt.

**Die Beschreibung** ist der Teil, den nur ein Mensch schreiben kann. DONE ordnet Aufgaben nach [Getting Things Done](../Z-anhang/Z010-glossar.md#getting-things-done), einer Methode, die Aufgaben aus dem Kopf in ein verlässliches System holt. Der Absatz zu den Bestandteilen nennt, woraus das System besteht: ein [Backend](../Z-anhang/Z010-glossar.md#backend), der Teil, der im Hintergrund auf einem zentralen Rechner läuft und die Daten hält, mit einer [WebAPI](../Z-anhang/Z010-glossar.md#webapi), einer Schnittstelle, über die Programme den Dienst über das Netz ansprechen. Darauf setzen die Zugänge: eine [PWA](../Z-anhang/Z010-glossar.md#pwa), ein Programm, das im Browser läuft und sich wie eine App auf dem Telefon installieren lässt; eine Webanwendung für den Schreibtisch; ein Kommandozeilen-Werkzeug für das [Terminal](../Z-anhang/Z010-glossar.md#terminal); ein [MCP-Server](../Z-anhang/Z010-glossar.md#mcp-server), der einem Agenten die Funktionen des Systems als Tools anbietet; und ein Bot, der in einem Messenger aus jeder Nachricht eine Aufgabe macht.

Der letzte Satz dieses Absatzes sagt, dass aus jedem Zugang später ein eigenes Projekt werden soll und dieses Projekt der [Koordinator](../Z-anhang/Z010-glossar.md#koordinator) ist. Das gehört zur Beschreibung, denn es ist ein Plan, den nur Sie kennen. Ohne diesen Satz schlägt der Agent ein einzelnes Projekt vor.

Der fachliche Kern darunter nennt in vier Punkten, was DONE von einer gewöhnlichen Aufgabenliste unterscheidet. Der Schluss sagt offen, dass der Prompt an vielen Stellen oberflächlich ist, und macht daraus einen Auftrag: nachfragen statt annehmen.

## Was er nicht enthält

Der Prompt greift dem Einrichten nichts vor. Die Anleitung sieht eine Reihe von Fragen vor, etwa ein Repo oder zwei, welches Kürzel, welche Sprache für Commits, und zum Schluss ein Konzept-Angebot. Keine dieser Fragen beantwortet der Prompt im Voraus. Sie kommen alle vom Agenten, und Sie antworten im Gespräch. So bleibt jedes Angebot der Vorlage erhalten. Dabei macht der Agent zu jeder Frage einen Vorschlag oder legt vor, was er aus der Beschreibung ableitet.

Auch die [Konzept-Sammlung](../Z-anhang/Z010-glossar.md#konzept-sammlung) nennt der Prompt nicht. Sie kommt aus dem Register der Vorlage, der Datei `wiki/Konzept-Repositories.md`, die mit dem Einrichten ins Projekt kommt. Dort liest der Agent, welche Sammlung er anbieten soll.

## Wie Sie ihn benutzen

Legen Sie einen leeren Ordner an und starten Sie darin Ihren Agenten. Sie brauchen dabei Internet, weil der Agent die Anleitung und die Vorlage von GitHub holt. Fügen Sie den Prompt als erste Nachricht ein. Im Terminal ist vorher nichts weiter zu tun.

Der Agent liest die Anleitung, bindet die Vorlage ein, kopiert die Projektdateien und legt den ersten Commit an. Dann zeigt er Ihnen seinen Fahrplan und bietet an, die Fragen einzeln mit Ihnen durchzugehen. Nehmen Sie das an. Was jede Frage bedeutet und was Sie für DONE antworten, steht in [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md). Die fachlichen Fragen kommen nach dem Einrichten.

Wenn Sie den Prompt für ein eigenes Projekt nehmen, ändern Sie die Beschreibung. Startsatz und Erlaubnis bleiben, ebenso der Schlusssatz, dass der Agent fachlich nachfragen soll. Alles ab „Das Projekt“ schreiben Sie für Ihr Vorhaben neu. Den Satz zum Koordinator nehmen Sie nur auf, wenn Ihr Projekt ebenfalls in mehrere Projekte zerfallen soll.

## Was jetzt klar sein sollte

- Ein Startprompt mit Referenzprozess hat drei Teile: den Startsatz, die Erlaubnis zum Ausführen und die Beschreibung des Projekts.
- Wie gearbeitet wird, steht nicht im Prompt. Das holt sich der Agent aus der Anleitung.
- Die Fragen des Einrichtens stehen ebenfalls nicht im Prompt. Sie kommen vom Agenten, und auch die Sammlung für das Konzept-Angebot kennt er aus dem Register der Vorlage.
- Für ein eigenes Projekt ändern Sie die Beschreibung. Dort darf der Prompt lückenhaft sein, wenn er dem Agenten sagt, dass er fragen soll.

Was derselbe Auftrag kostet, wenn man dem Agenten alles selbst erklärt, zeigt [DONE ohne Regelwerk](Y030-done-ohne-regelwerk.md). Wie der Agent mit diesem Prompt das Projekt aufsetzt, zeigt Schritt für Schritt [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md).
