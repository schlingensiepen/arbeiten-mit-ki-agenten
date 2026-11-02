# Subagenten

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `wiki/Angebots-und-Beauftragungs-Muster.md`.

Das [Kontextfenster](../Z-anhang/Z010-glossar.md#kontextfenster) ist begrenzt, das wissen Sie aus dem Kapitel [Kontext](../A-verstehen-und-loslegen/A020-kontext.md). Jede Datei, die der Agent liest, landet darin und bleibt dort. Eine Recherche, die zehn lange Seiten durchgeht, füllt das Fenster mit Material, von dem Sie am Ende nur das Ergebnis brauchen. Der [Subagent](../Z-anhang/Z010-glossar.md#subagent) ist die einfachste Antwort darauf: Ein Schritt des Plans geht an einen zweiten Agenten mit leerem Fenster, und zurück kommt nur sein Ergebnis. Dieses Kapitel zeigt, was ein Subagent ist, wie sein Auftrag zu ihm kommt und wo er an seine Grenze stößt. Es ist zugleich der erste Schritt von einem Agenten zu mehreren, dem Thema dieses Teils.

## Was ein Subagent ist

Ein Subagent ist ein Agent, den der [Harness](../Z-anhang/Z010-glossar.md#harness) aus einem laufenden Gespräch heraus startet. Technisch ist er ein weiteres [Tool](../Z-anhang/Z010-glossar.md#tool): Das Modell fordert es an wie das Lesen einer Datei, nur dass dieses Tool einen ganzen zweiten Agenten anwirft. Welches Modell und welche Tools er bekommt, hängt vom Harness ab (Stand Oktober 2026). Sein Fenster ist in jedem Fall leer. Er kennt Ihr Gespräch nicht, er kennt nur den einen Prompt, den er mitbekommt. Damit durchläuft er seine eigene Schleife aus Prompt, Antwort, Tool-Aufruf und Ergebnis, wie in [Was ein Agent ist](../A-verstehen-und-loslegen/A010-was-ein-agent-ist.md) beschrieben, und gibt am Ende einen Text an den Agenten zurück, der ihn gestartet hat.

Entscheidend ist, was wo landet. Alles, was der Subagent liest, bleibt in seinem Fenster, und das wird nach seiner Rückkehr weggeworfen. In Ihrem Fenster kommt nur sein Rückgabetext an. Aus einer Recherche über zehn Seiten werden so zwanzig Zeilen Ergebnis. Das Regelwerk nennt ihn an manchen Stellen auch Unteragent, gemeint ist dasselbe.

Ob Ihr Harness Subagenten starten kann, steht in dessen Dokumentation. Die Arbeitsweise dieses Skripts setzt es voraus, denn das Regelwerk lässt Prüfungen und Recherchen von Subagenten erledigen.

## Warum: das Fenster schonen

Eine Recherche muss nicht im eigenen Fenster laufen: Ein anderer Agent macht sie und liefert das Ergebnis. Das ist der erste Gewinn. Ihr Fenster bleibt frei für die eigentliche Arbeit, und was der Subagent an Material durchgesehen hat, verdrängt später nichts, was Sie noch brauchen. Umfangreiche Fundstellen, etwa Handbücher oder Normtexte, lässt das Regelwerk deshalb grundsätzlich von Subagenten auswerten, statt sie vollständig in das eigene Fenster zu laden.

Der zweite Gewinn ist weniger offensichtlich. Der Subagent fängt frisch an, ohne den Ballast und ohne die Annahmen Ihres Gesprächs. Wer eine Stunde lang an einer Spezifikation geschrieben hat, liest über ihre Lücken hinweg; ein Agent, der sie zum ersten Mal sieht, nicht. Genau darum lässt das Regelwerk Prüfer in frischem Kontext starten. Wie eine solche Prüfung abläuft, steht im Kapitel [Prüfen](../G-der-gesamtprozess/G020-pruefen.md); dieses Kapitel liefert den Mechanismus, mit dem ein Prüfer gestartet wird.

## Der Auftrag ist eine Datei

Der Subagent weiß nichts außer dem, was in seinem Prompt steht. Das macht den Auftrag zur eigentlichen Arbeit. Daraus folgt eine Regel: Sein Arbeitsauftrag ist eine Datei auf der Platte. Der Prompt an den Subagenten sagt dann nur noch, wo diese Datei liegt und wohin das Ergebnis soll. Das Regelwerk legt für solche Aufträge einen festen Rahmen fest:

1. **Vorher liegt alles auf der Platte.** Was der Subagent wissen muss, steht in Dateien, nicht in Ihrem Chat. Er liest nur die Platte, Ihr Gespräch kann er nicht sehen.
2. **Die Zieldatei steht im Auftrag.** Genauer Pfad und Dateiname, dazu die erwartete Gliederung. Die Anweisung lautet: Schreibe genau diese eine Datei.
3. **Schreibgrenzen.** Nur diese eine Datei, kein Commit, nichts anderes anfassen. Was er lesen soll, nennt der Auftrag ausdrücklich als nur zu lesen.
4. **Der Rückgabetext ist Zusammenfassung, nicht Träger.** Eine Ampel und wenige Sätze; das Ergebnis lebt in der Datei. Der Rückgabetext landet in Ihrem Fenster, deshalb bleibt er kurz. Die Datei dagegen kann jeder später lesen, auch eine spätere Sitzung.
5. **Nummern vergibt der Auftraggeber.** Soll das Ergebnis als Element in ein [Register](../Z-anhang/Z010-glossar.md#register) eingehen, vergibt der Hauptagent die Nummer vor dem Start und trägt das Element nach der Rückkehr ein. Der Subagent schreibt nie selbst ins Register.

Für eine Recherche nennt das Regelwerk zusätzlich die Bausteine des Auftrags: die Frage samt dem Schritt, für den die Antwort gebraucht wird, denn daran bemisst sich, wann sie reicht; der Rahmen der erlaubten Quellen und Werkzeuge; keine erhoffte Antwort im Auftrag, damit der Subagent nicht findet, was er finden soll; die Ehrlichkeitsregeln, nach denen Fund und Nicht-Fund getrennt bleiben, „nichts Belastbares gefunden“ ein gültiges Ergebnis ist, nichts erfunden wird und jede Aussage ihre Quelle mit Datum trägt; und das Lieferformat, damit Sie das Ergebnis mechanisch übernehmen können.

## Beispiel DONE: eine Recherche zur Methode

DONE baut auf der Methode [Getting Things Done](../Z-anhang/Z010-glossar.md#getting-things-done) auf. Angenommen, beim Schreiben der Anforderungen kommt die Frage auf, wie die Methode mit Aufgaben umgeht, die an einen Termin gebunden sind. Die Antwort braucht einen Blick in die Literatur, und den soll nicht Ihr Hauptagent tun. Sie legen die Datei `auftrag.md` an, oder lassen sie den Agenten anlegen:

```markdown
# Recherche: Termine in Getting Things Done

## Frage und Zweck
Wie behandelt die Methode Aufgaben mit festem Termin, im Unterschied
zu Aufgaben ohne Termin? Gebraucht für die Anforderungen an DONE:
Wir müssen entscheiden, ob eine Aufgabe ein Datum trägt.

## Quellen
Öffentlich zugängliche Beschreibungen der Methode. Keine Foren.

## Regeln
Fund und Nicht-Fund trennen. Nichts erfinden. Jede Aussage mit
Quelle und Datum. „Nichts Belastbares gefunden“ ist ein gültiges
Ergebnis.

## Lieferung
Schreibe genau die Datei bericht.md mit den Abschnitten Frage,
Verlauf, Fundstellen, Ergebnis. Ändere keine andere Datei, kein
Commit. Rückmeldung: Ampel und höchstens drei Sätze.
```

Dann der Prompt an den Hauptagenten:

```text
Starte einen Subagenten. Sein Auftrag steht in auftrag.md, seinen Bericht schreibt er nach bericht.md.
```

Was jetzt passiert: Der Hauptagent ruft das Tool für Subagenten auf und gibt ihm einen kurzen Prompt mit, der auf die beiden Dateien zeigt. Der Subagent liest `auftrag.md`, sucht, liest, verwirft, liest weiter, und schreibt `bericht.md`. Zurück kommt etwa: „Grün. Drei Fundstellen, die Methode unterscheidet terminierte Aufgaben im Kalender von allen anderen. Eine Stelle widerspricht, siehe Abschnitt Verlauf.“ Ihr Fenster ist um zwei kurze Texte gewachsen, um den Prompt und um die Rückmeldung. Alles, was der Subagent gelesen hat, ist nicht darin.

Das Ergebnis ist eine Fremdaussage. Ob es in die Anforderungen von DONE eingeht, entscheiden Sie, nicht der Subagent und nicht der Hauptagent. Das Regelwerk hält diese Übernahme als Entscheidung fest. Bis dahin ist das Ergebnis ein Nachweis, nicht die Wahrheit des Projekts, wie im Kapitel [Prüfen](../G-der-gesamtprozess/G020-pruefen.md) beschrieben.

## Von einem Agenten zu mehreren

Der Subagent ist der erste Schritt von einem Agenten zu mehreren, aber ein begrenzter. Er lebt nur so lange wie sein Auftrag. Er läuft innerhalb Ihres Harness, in Ihrer Sitzung. Sie sehen ihn nicht arbeiten und können ihm zwischendurch nichts sagen. Und er berichtet nur dem Agenten, der ihn gestartet hat. Für eine Recherche oder eine Prüfung ist das genau richtig: klar umrissen, Ergebnis in einer Datei, fertig.

Für anderes reicht es nicht. Wenn ein zweiter Agent über Stunden neben Ihrem arbeiten soll, in einem eigenen Fenster, in das Sie hineinsehen können, und das Ihre Sitzung überlebt, dann braucht er einen eigenen Prozess. Das ist das nächste Kapitel. Und wenn zwei solche Agenten sich untereinander abstimmen müssen, brauchen sie einen Weg, einander Nachrichten zu schicken. Das ist das übernächste.

## Was jetzt klar sein sollte

- Ein Subagent ist ein Agent, den der Harness aus dem Gespräch heraus startet, mit leerem Fenster; Modell und Tools hängen vom Harness ab. Zurück kommt nur sein Ergebnis.
- Er schont Ihr Fenster, weil alles, was er liest, bei ihm bleibt. Und er sieht frisch, weil er Ihre Annahmen nicht kennt; darum prüft man mit ihm.
- Sein Auftrag ist eine Datei auf der Platte. Der Auftrag nennt die Zieldatei, die Schreibgrenzen und die Regeln, der Rückgabetext bleibt kurz.
- Er lebt nur für seinen Auftrag und berichtet nur seinem Auftraggeber. Für parallele Arbeit im eigenen Fenster braucht es einen zweiten Agenten als eigenen Prozess.

Weiter mit [peeragent](H020-peeragent.md): Wie ein zweiter Agent als eigener Prozess startet und was er braucht, um arbeiten zu können.
