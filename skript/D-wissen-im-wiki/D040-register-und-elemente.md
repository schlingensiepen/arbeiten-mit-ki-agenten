# Register und Elemente

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `Wiki.md`, `docs/Wiki-und-Register.md`.

Viele Fassaden des Wikis sind Register: Listen mit nummerierten Einträgen, dahinter je ein Detail-Knoten. Anforderungen, Entscheidungen, Fehlermeldungen, Testfälle, alles läuft nach demselben Muster. Dieses Kapitel erklärt das Muster an den Entscheidungen: warum eine Festlegung eine Nummer und eine Begründung bekommt, was passiert, wenn sie sich ändert, und warum nichts davon jemals gelöscht wird. Neu ist daran wenig. Das Software Engineering kennt das Werkzeug seit Langem als Decision Record: Man schreibt auf, was entschieden wurde, im Prinzip ein großer Log. Agenten brauchen nichts anderes, nur konsequenter.

## Was ein Register ist

Ein [Register](../Z-anhang/Z010-glossar.md#register) ist eine Fassade mit einer Zeile je Eintrag. Wo ein Eintrag mehr trägt als eine Zeile, etwa verworfene Alternativen oder eine ausführliche Begründung, bekommt er einen eigenen Detail-Knoten. Jeder Eintrag hat eine Kennung aus einem Präfix und einer laufenden Nummer: Entscheidungen heißen `DEC-`, Ideen `IDEA-`, der Software-Prozess bringt `REQ-` für Anforderungen, `BUG-` für Fehlermeldungen, `TEST-` für Testfälle und weitere mit. Eine Kennung wird nie wiederverwendet. Lücken bleiben.

Die Einträge sind von zweierlei Art. [Elemente](../Z-anhang/Z010-glossar.md#element) sind Einträge, die abgelöst werden können und in Freigabedokumente eingehen: Entscheidungen, Ideen, Anforderungen, Marken. Nachweise werden nie abgelöst, nur mit Vermerken ergänzt: Berichte von Prüfern, Rechercheergebnisse, eingegangene Dokumente. Dazu kommen lebende Dinge ohne Einfrieren wie das Glossar oder die Rollen; die werden für ein Freigabedokument kopiert, wie das Kapitel [Freigabedokument: Sammler und Freezer](../F-marken-und-freigaben/F020-freigabedokument-sammler-und-freezer.md) zeigt.

## Eine Entscheidung bekommt eine Nummer und eine Begründung

Eine [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) ist eine festgelegte Projekt-Wahrheit. Ihr Eintrag nennt die Wahl, die Begründung, die verworfenen Alternativen und Verweise auf das, worauf sie sich stützt, dazu die Marke, für die sie gilt, und das Datum. Sie kommt erst mit Ihrem OK ins Register, und zwar direkt als angenommen; Entwürfe liegen nie im Wiki. Vor jeder neuen Entscheidung durchsucht der Agent das Register nach verwandten Einträgen und nennt sie Ihnen. So kann ein Eintrag für DONE aussehen:

```markdown
### DEC-7 — Delegierte TODOs bleiben auf beiden Seiten

- **Status:** angenommen
- **Zielmarke:** 1.0
- **Angelegt:** 2026-10-20
- **Wahl:** Beim Delegieren entstehen zwei verlinkte TODOs, eines je Benutzer.
- **Begründung:** Beide wollen sehen, wie weit es ist. Der Empfänger ordnet mit
  eigenen Tags, der Absender behält die Frist im Blick.
- **Verworfen:** Ein gemeinsamer Eintrag für beide. Dann müssten sich beide
  auf Tags und Sichten einigen.
```

Warum der Aufwand? Weil diese Entscheidung die Voraussetzung für die nächsten ist. Die Funktionsbeschreibung des Delegierens, das Datenmodell, die Testfälle: Alle stützen sich darauf, dass es zwei TODOs gibt. Wer in drei Monaten fragt, warum das so ist, findet die Nummer in jedem dieser Dokumente und die Begründung im Register. Und wenn der Agent behauptet, das sei so entschieden, nennt er die Nummer. Ohne Nummer ist es eine Erinnerung, und die wird erst geprüft.

Die Nummer ist dabei mehr als eine Ordnungszahl. Ab der Annahme ist der Inhalt des Eintrags eingefroren; die Nummer zeigt heute und in einem Jahr auf denselben Text. Nur das macht sie zitierfähig.

## Festlegung, Vertagung und der Preis einer Entscheidung

Drei Arten von Einträgen begegnen Ihnen besonders oft.

**Die Festlegung.** Eine Festlegung ist eine Entscheidung, die man jetzt trifft, damit es weitergeht, und die bei neuem Bedarf geändert werden kann. Für DONE etwa: Tags lösen die Kategorien der Methode ab; was keinen Tag hat, liegt in der Inbox. Das gilt für die erste Marke. Stellt sich später heraus, dass es nicht reicht, wird es geändert, aber nicht durch Überschreiben, sondern wie im nächsten Abschnitt beschrieben.

**Die Vertagung.** Manche Entscheidung will man jetzt nicht treffen: „Das machen wir für eine Version 3.“ Eine nicht getroffene Entscheidung ist keine Entscheidung, sondern eine Idee mit einem Auslöser, einem Datum oder einer Marke. Für DONE: Der Messenger-Bot, der aus jeder Nachricht eine Aufgabe macht, kommt ins Ideen-Register mit dem Auslöser Marke 3.0. Wird der Auslöser fällig, holt der Agent den Eintrag beim Sessionstart von selbst wieder hervor. Vertagen ist also auch ein Eintrag, kein Vergessen.

**Die Entscheidung mit genanntem Preis.** Eine gute Entscheidung sagt, was sie kostet. Für DONE: Erledigte TODOs werden nicht gelöscht, sondern als erledigt markiert. Der Preis: Die Datenmenge wächst, und jede Sicht muss Erledigtes ausblenden. Der Gewinn: Verweise aus delegierten TODOs und aus gespeicherten Sichten bleiben gültig. Wer den Preis aufschreibt, erspart dem nächsten Leser die Frage, ob man daran gedacht hat.

## Ablösen und Verwerfen statt Löschen

Was angenommen ist, wird nicht mehr geändert. Ändert sich die Sache, entsteht ein neues Element mit neuer Nummer, das das alte ablöst; beide tragen den Verweis aufeinander, und das alte bleibt sichtbar stehen. Was eine Entscheidung nur präzisiert, ohne sie zu ändern, wird als Vermerk angehängt. Das Regelwerk nennt das [Ablösung](../Z-anhang/Z010-glossar.md#ablösung). So bleibt datierbar, was wann galt.

Eine zweite Form ist das [Verwerfen](../Z-anhang/Z010-glossar.md#verwerfen): Ein Element wird mit Begründung aufgegeben, ohne Nachfolger. Auch dann bleibt es stehen, und seine Nummer bleibt vergeben.

Der Gedanke dahinter ist derselbe wie beim Artikel in der Lagerverwaltung. Ein Artikel, der nicht mehr geführt wird, wird nicht gelöscht, sondern inaktiv gesetzt. Denn jede Buchung der Vergangenheit verweist auf ihn: von welchem Fach in welches Fach, welcher Artikel. Löscht man den Artikel, stimmen die Buchungen nicht mehr. Setzt man ihn inaktiv, bleibt das Archiv intakt, und der Eintrag stimmt noch in tausend Jahren.

Mit Elementen ist es genauso. Nehmen Sie an, für DONE gilt in Marke 2.0 die Anforderung, dass Sichten nach Tags, Terminen und Text filtern. Die Funktionsbeschreibung für 2.0 verweist auf diese Anforderung. Für Marke 3.0 wünscht sich jemand zusätzlich Filter nach Personen. Dann wird die Anforderung nicht umgeschrieben, sondern durch eine neue abgelöst, die für 3.0 gilt. Die Funktionsbeschreibung für 2.0 bleibt sinnvoll, weil die alte Anforderung weiter dasteht und weiter dasselbe sagt. Hätte man sie überschrieben, würde die Beschreibung von 2.0 plötzlich auf einen Text zeigen, den es zur Zeit von 2.0 nicht gab.

## Was jetzt klar sein sollte

- Ein Register ist eine Liste nummerierter Einträge mit Detail-Knoten dahinter. Eine Kennung wird nie wiederverwendet.
- Eine Entscheidung trägt Wahl, Begründung und verworfene Alternativen, kommt erst mit Ihrem OK ins Register und ist ab dann eingefroren. Die Nummer macht sie zitierfähig.
- Festlegen heißt jetzt entscheiden, Vertagen heißt eine Idee mit Auslöser anlegen, und eine gute Entscheidung nennt ihren Preis.
- Geändert wird durch Ablösen, aufgegeben durch Verwerfen. Gelöscht wird nichts, damit alles, was sich auf ein Element bezieht, gültig bleibt.

Weiter mit [Wer entscheidet was](../E-mensch-und-agent/E010-wer-entscheidet-was.md): welche Entscheidungen der Agent selbst trifft und welche nur Sie treffen können.
