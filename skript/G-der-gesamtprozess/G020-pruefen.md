# Prüfen

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `Reviewmuster.md`, `docs/Arbeitsweise.md`, `tools/lint.sh`.

> **In zwanzig Minuten schafft man es, eine Spezifikation zu schreiben, die sich selbst widerspricht. Leider ist das eher der Regelfall als die Ausnahme.**

Der Agent schreibt Anforderungen, Beschreibungen, Spezifikationen, und er schreibt sie schnell. Fragt man ihn, ob die Fachlogik klar ist, sagt er ja. Die eigentliche Frage ist, ob sie uns klar ist, und ob das, was dasteht, zusammenpasst. Am Anfang glaubt man dem Agenten; im Lauf des Semesters lernt man, es zu hinterfragen. Dieses Kapitel gibt Ihnen das Werkzeug dafür. Es erklärt zwei Arten von Prüfung: den [Lint](../Z-anhang/Z010-glossar.md#lint), ein Programm ohne Modell, das Formfehler findet, und das [Review](../Z-anhang/Z010-glossar.md#review), bei dem ein zweites Modell mit frischem Kontext liest. Dazu kommt, was Sie tun, wenn Sie nur ein Modell haben, und warum Sie dem Prüfer zusehen sollten.

## Der Lint: ein Programm ohne Modell

Bevor ein Modell liest, läuft ein Programm. Der Lint liegt in der Vorlage und wird aus dem Projektordner aufgerufen:

```sh
sh _template/tools/lint.sh
```

Er prüft, was sich ohne Sprachmodell prüfen lässt: Hat jeder Knoten im Wiki den Kopf, den sein Typ verlangt, mit allen Pflichtfeldern? Zeigt jeder Link auf eine Datei, die es gibt? Ist jede Nummer im Register nur einmal vergeben? Verweist eine Ablösung in beide Richtungen, vom alten auf das neue Element und zurück? Steht ein Freigabe-Eintrag in der festen Form, an der das Regelwerk ihn erkennt? Enthält ein Dateiname Umlaute? Jeder Befund trägt einen Code, und der Lint unterscheidet Fehler von Hinweisen. Ein Hinweis ist etwa ein älteres Element, dem ein Feld fehlt, das es damals noch nicht gab.

Was der Lint nicht tut: den Inhalt beurteilen. Ob eine Anforderung sinnvoll ist, ob zwei Anforderungen sich widersprechen, ob die Spezifikation die Funktionsbeschreibung trifft, sieht er nicht. Er ist deshalb kein Ersatz für das Review, sondern dessen Vorstufe. Dafür ist er billig und deterministisch: Er braucht keinen Kontext und liefert bei gleichem Eingang immer dasselbe Ergebnis. Der Agent ruft ihn zu festen Anlässen von sich aus auf, und Sie können ihn jederzeit selbst starten.

## Warum ein zweites Modell draufschaut

Die Sitzung, die ein Dokument geschrieben hat, ist die schlechteste Prüferin dafür. In ihrem [Kontext](../Z-anhang/Z010-glossar.md#kontext) liegt das ganze Gespräch: was gemeint war, was verworfen wurde, welche Lücke man später schließen wollte. Liest diese Sitzung ihr eigenes Dokument, liest sie mit, was nicht dasteht. Der nächste, der mit dem Dokument arbeitet, hat das alles nicht. Er hat nur die Datei.

Deshalb prüft ein Prüfer mit frischem Kontext. Er kennt das Gespräch nicht, er bekommt nur den Auftrag und die Datei, und er liest sie so, wie jeder spätere Leser sie liest. Genau so entstand der Satz am Anfang des Kapitels: Ein Agent hatte in kurzer Zeit Anforderungen geschrieben, ein zweiter Agent mit leerem Kontext bekam nur den Auftrag und die Datei, und er fand Stellen, die sich widersprachen. Dabei zeigte sich auch, was ein guter Prüfer leistet: Er trennt den echten Widerspruch von der Lücke und beide vom Scheinbefund.

Das Regelwerk geht einen Schritt weiter als der frische Kontext. Die [Zwei-Modelle-Regel](../Z-anhang/Z010-glossar.md#zwei-modelle-regel) verlangt je Prüfrunde mindestens zwei unabhängige Prüfer, und unabhängig heißt: verschiedene Modelle, je ein eigener, frischer Kontext. Zwei Läufe desselben Modells zählen nicht als zwei Prüfer. Die Grundregel dahinter lautet: Das Modell, das prüft, ist nicht das Modell, das gebaut hat. Bei Menschen entspricht dem die Regel, dass zwei Personen prüfen, die am Text nicht mitgeschrieben haben.

## Der Standard-Prüfprompt

Jeder Prüfer bekommt dieselben Fragen. Das Regelwerk nennt sie den Standard-Prüfprompt:

1. Was leitest du daraus als deinen Auftrag ab? Ausdrücklich nicht: Fasse zusammen.
2. Wie würdest du auf dieser Grundlage konkret vorgehen? Mit einem realistischen Beispiel, das je Lauf wechselt.
3. Welche Widersprüche, Lücken und Mehrdeutigkeiten findest du? Mit der Aufforderung, keine Probleme zu erfinden und saubere Bereiche als sauber zu benennen.
4. Eine vierte, fachliche Frage, wenn der Prozess sie vorsieht. Für die Funktionsbeschreibung etwa: Ist sie frei von Vorannahmen über die Technologie?

Die ersten beiden Fragen sind keine Aufwärmübung. Eine Zusammenfassung beweist nur, dass der Prüfer gelesen hat. Der abgeleitete Auftrag und das durchgespielte Beispiel zeigen, was er verstanden hat, und an dieser Stelle fallen Lücken auf, die beim bloßen Lesen unsichtbar bleiben. Die dritte Frage trägt ihre Gegenregel in sich: Ein Prüfer, der Probleme erfinden darf, liefert immer welche.

Das Ergebnis ist ein Bericht. Jeden Befund stuft der Prüfer selbst ein: entscheidungsbedürftig, also ein echter Widerspruch oder eine echte Lücke, die vor der Freigabe behandelt werden muss; eine Frage der Formulierung; oder akzeptabel, weil der Prüfer nur die Absicht des Dokuments nicht getroffen hat. Diese Einstufung ist ein Vorschlag. Der Agent, der die Prüfung koordiniert, entscheidet sie abschließend, bei Grenzfällen Sie, und eine Abweichung vom Vorschlag wird begründet. Darüber steht die [Ampel](../Z-anhang/Z010-glossar.md#ampel), das Gesamturteil des Prüfers: grün, gelb oder rot. Der Bericht wird als Knoten im Wiki abgelegt und im Register der Agent-Berichte geführt, zusammen mit dem Modell, das geprüft hat, und dem Modell, das gebaut hat. So bleibt die Zwei-Modelle-Regel später nachprüfbar.

## Prüfen, Einarbeiten, Re-Check

Ein Review ist selten mit einer Runde fertig. Liefert eine Runde entscheidungsbedürftige Befunde, arbeitet der Agent sie ein, und dann folgt eine neue Runde: wieder unabhängige Prüfer, wieder frischer Kontext. Diese erneute Prüfung heißt [Re-Check](../Z-anhang/Z010-glossar.md#re-check). Reif ist ein Dokument, wenn eine Runde keinen entscheidungsbedürftigen Befund mehr liefert. Befunde zur Formulierung zählen nicht dagegen. Bei hohem Risiko, etwa bei Fragen der Sicherheit oder bei Dokumenten, die an Dritte gehen, gilt ein Dokument erst als reif, wenn zwei oder drei Runden in Folge nichts Neues bringen.

![Links ein grüner Block Anforderungen, das geprüfte Dokument. Ein schwarzer Pfeil führt zu einem blauen Block Lint, Programm ohne Modell. Von dort führen zwei schwarze Pfeile zu zwei übereinander stehenden blauen Blöcken Prüfer A, Modell 1, frischer Kontext, und Prüfer B, Modell 2, frischer Kontext. Beide zeigen auf einen gelben Block Bericht, Befunde und Ampel. Ein oranger Pfeil führt vom Bericht hinunter zu einem blauen Block Einarbeiten, Befunde ins Dokument, und von dort links herum zurück zum Dokument, beschriftet: Re-Check, neue Runde, bis kein Befund mehr entscheidungsbedürftig ist.](bilder/G020-review-schleife.svg)

**Prüfen, Einarbeiten, Re-Check.** Das Dokument geht erst durch den Lint, dann parallel an zwei Prüfer verschiedener Modelle mit frischem Kontext. Ihr Bericht wird eingearbeitet, und die nächste Runde beginnt mit neuen Prüfern, bis kein Befund mehr entscheidungsbedürftig ist.

Die Schleife hat eine Obergrenze. Liefert die dritte Runde immer noch entscheidungsbedürftige Befunde, endet das Review nicht mit einer Freigabe, sondern mit einem Bericht an Sie: welche Befunde wiederkehren und ob ihre Ursache im Dokument liegt oder in einer Regel oder Entscheidung dahinter. Ihre Möglichkeiten stehen dabei: eine weitere Runde nach Anpassung, eine Änderung an der Regel, eine Notfall-Freigabe mit der Zusage, sie durch ein reifes Freigabedokument abzulösen, oder Abbruch. Kehrt ein Befund nach dem Einarbeiten in gleicher Form wieder, legt der Agent ihn Ihnen sofort vor, ohne die dritte Runde abzuwarten. Eine Freigabe ohne Reife gibt es nur als Ihre Entscheidung, nie als Ausweg des Agenten.

## Wenn es nur ein Modell gibt

Ein zweites Modell kommt nicht von allein in die Sitzung. Der Agent braucht dafür ein Werkzeug: einen zweiten Agenten mit einem anderen Modell, den er als eigenen Prozess startet, oder einen Zugang zu einem externen Modell. Wie man einen zweiten Agenten startet, zeigt das Kapitel [peeragent](../H-mehrere-agenten/H020-peeragent.md); wie der Agent Prüfer mit frischem Kontext startet, das Kapitel [Subagenten](../H-mehrere-agenten/H010-subagenten.md). Welches Werkzeug ein Projekt dafür benutzt, steht in seiner Werkzeugliste.

Fehlt ein solches Werkzeug, gilt der Ersatzweg, den Sie beim Aufsetzen des Projekts gewählt haben. Es gibt zwei:

- **Der Ein-Modell-Weg.** Dasselbe Modell prüft in frischem Kontext. Der Bericht hält fest, dass Prüf-Modell und Bau-Modell dasselbe sind, und der Eintrag der Freigabe nennt diese Einschränkung. Das ist schwächer als die Zwei-Modelle-Regel, und das Regelwerk sagt das so.
- **Sie als Prüfer.** Eine Person, die nicht mitgeschrieben hat, prüft selbst; der Bericht hält ihr Urteil fest.

Ohne jedes Zusatzwerkzeug bleibt nur der Ein-Modell-Weg, und Sie können ihn von Hand gehen: Öffnen Sie eine zweite, frische [Sitzung](../Z-anhang/Z010-glossar.md#sitzung), so wie in [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md) beschrieben, und geben Sie ihr die Datei und die vier Fragen. Die zweite Sitzung kennt das Gespräch der ersten nicht. Das ist der frische Kontext; es ist nicht das zweite Modell. DONE hat beim Aufsetzen genau das festgelegt: Ein-Modell-Weg, falls der Agent kein zweites Modell erreicht.

## Verantwortung und Grenzen

> **Die allerbeste KI für einen Benchmark ist die, die die Ergebnisse kennt.**

Der Satz sagt, was ein Modell tut, wenn man es lässt: Es nimmt den kürzesten Weg zum Ziel, auch wenn der Weg die Prüfung aushöhlt. Für die Prüfung heißt das: Ein Prüfer, der weiß, was der Autor wollte und was herauskommen soll, bestätigt es ihm. Darum der frische Kontext, darum das andere Modell, darum die Aufforderung, keine Probleme zu erfinden und saubere Bereiche als sauber zu benennen. Jede dieser Regeln nimmt dem Prüfer eine Abkürzung.

Es gibt Dinge, die kein Prüfer Ihnen abnimmt. Die Freigabe ist Ihre. Die Einstufung eines Befunds in Grenzfällen ist Ihre. Ein Vorschlag des Prüfers ist ein Vorschlag; Sie dürfen ihn verwerfen und einen besseren nehmen. Was ein Prüfer oder eine Recherche von außen beibringt, ist ein Nachweis, nicht die Wahrheit des Projekts; ob es übernommen wird, entscheiden Sie. Und darum lohnt es sich, dem Prüfer zuzusehen: Sein Bericht liegt als Datei im Wiki, bevor der Agent ihn zusammenfasst. Lesen Sie den Bericht, nicht nur die Zusammenfassung. Dort steht, was der Prüfer wirklich geprüft hat.

## Beispiel: Ein zweites Modell prüft die Anforderungen von DONE

Die Anforderungen zur Marke 1.0 von DONE sind als Elemente angenommen, das Freigabedokument ist gebildet. Bevor es „für P4 Beschreiben der Funktion“ freigegeben wird, läuft die Prüfung.

Zuerst der Lint. Er meldet, dass einem Element die Marke fehlt, und einen Link, der auf einen umbenannten Knoten zeigt. Beides ist in einer Minute behoben. Dann der Lauf erneut, ohne Fehler.

Dann die Prüfer. Hat der Agent ein zweites Modell über ein Werkzeug, bekommen zwei Prüfer verschiedener Modelle die Datei und die vier Fragen; sonst zwei frische Sitzungen desselben Modells, mit Vermerk. Prüfer A leitet als Auftrag ab: eine Aufgabenverwaltung für mehrere Benutzer mit Delegation und berechneten Fristen. Als Beispiel spielt er durch, wie ein Benutzer ein TODO ohne Tag an einen Kollegen delegiert. Dabei fragt er: Eine Anforderung sagt, was keinen Tag hat, liegt in der Inbox. Beim Delegieren entsteht auf der anderen Seite ein eigenes TODO. Liegt es in der Inbox des Empfängers, in der des Absenders oder in beiden? Die Anforderungen sagen es nicht. Lücke, entscheidungsbedürftig. Prüfer B findet denselben Punkt und zusätzlich einen Widerspruch: Deadlines werden aus Abhängigkeiten berechnet, aber ein delegiertes TODO darf vom Empfänger gelöscht werden; was geschieht dann mit der Deadline, die davon abhing? Beide Ampeln stehen auf gelb.

Der Agent legt die Befunde vor. Sie entscheiden: Das delegierte TODO liegt in der Inbox des Empfängers; ein gelöschtes TODO bleibt als Abhängigkeit sichtbar und wird als erledigt gewertet. Beide Festlegungen werden neue Anforderungen, die alten Elemente werden abgelöst, das Freigabedokument wird neu gebildet. Dann der Re-Check mit zwei frischen Prüfern. Keine entscheidungsbedürftigen Befunde mehr, beide Ampeln grün. Jetzt wird das Dokument freigegeben, und der Eintrag der Freigabe verweist auf die beiden Berichte.

## Was jetzt klar sein sollte

- Der Lint ist ein Programm ohne Modell. Er findet Formfehler: fehlende Felder, tote Links, doppelte Nummern. Den Inhalt beurteilt er nicht, und er läuft vor jedem Review.
- Ein Review braucht frischen Kontext, weil die schreibende Sitzung mitliest, was nicht dasteht. Die Zwei-Modelle-Regel verlangt dazu zwei Prüfer verschiedener Modelle.
- Jeder Prüfer beantwortet den Standard-Prüfprompt: Auftrag ableiten, Vorgehen durchspielen, Widersprüche und Lücken nennen, ohne welche zu erfinden. Sein Urteil ist die Ampel.
- Prüfen, Einarbeiten, Re-Check, bis kein Befund mehr entscheidungsbedürftig ist, höchstens drei Runden. Dann entscheiden Sie.
- Ohne zweites Modell gilt der Ein-Modell-Weg, notfalls als zweite frische Sitzung von Hand. Das ist schwächer, und es wird gesagt.

Weiter mit [Werkstatt, Produkt, Schleuse](G030-werkstatt-produkt-schleuse.md): Warum manche Projekte zwei Repos haben und was beim Übergang vom einen ins andere geschieht.
