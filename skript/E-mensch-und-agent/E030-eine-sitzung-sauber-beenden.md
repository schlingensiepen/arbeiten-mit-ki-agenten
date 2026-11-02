# Eine Sitzung sauber beenden

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Arbeitsweise.md`.

Eine [Sitzung](../Z-anhang/Z010-glossar.md#sitzung) hat ihren eigenen [Kontext](../Z-anhang/Z010-glossar.md#kontext), und der ist weg, wenn sie endet. Das haben Sie im Kapitel [Kontext](../A-verstehen-und-loslegen/A020-kontext.md) gesehen. Alles, was Sie in dieser Sitzung mit dem Agenten geklärt haben und das nur im Chat steht, ist dann verloren. Die nächste Sitzung beginnt mit leerem Kontext und liest Dateien. Sie kann nur fortsetzen, was in Dateien steht. Dieses Kapitel zeigt, was vor dem Ende einer Sitzung in die Dateien muss und wer das tut.

## Der Zustand, den die nächste Sitzung braucht

Das Ziel ist im Regelwerk genau benannt: Vor jedem Übergabe-Moment stellt der Agent den Zustand her, in dem ein fremder Agent allein aus den Dateien nahtlos übernehmen könnte. Fremd heißt: ohne das Gespräch gelesen zu haben, vielleicht ein anderes Modell, vielleicht in einem Monat. Übergabe-Momente sind das Ende oder die Pause einer Sitzung, Ihre Aufforderung dazu, etwa „Speicherpunkt setzen“, und der Start eines [Subagenten](../Z-anhang/Z010-glossar.md#subagent), der ebenfalls nur die Dateien sieht.

Dass die nächste Sitzung dann wirklich weitermachen kann, liegt am [Sessionstart](../Z-anhang/Z010-glossar.md#sessionstart) aus [Regelwerk und Sessionstart](../D-wissen-im-wiki/D020-regelwerk-und-sessionstart.md): Der Agent liest beim Start den Arbeitsstand und meldet sich mit Erledigt, Aktion, Frage. Beide Enden passen zusammen. Das Ende der einen Sitzung schreibt, was der Anfang der nächsten liest.

## Vier Schritte

**Klärungen ins Wiki.** Was Sie im Gespräch geklärt haben, wandert in eine Datei. Eine neue Projekt-Wahrheit wird eine [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) im Register, eine Klarstellung zu einem Begriff ein Vorschlag für das Glossar, ein Hinweis gegen ein hartnäckiges Fehlverständnis des Agenten ein Eintrag in `wiki/Facts.md`, Letzteres nur auf Ihre ausdrückliche Anweisung. Nicht „das machen wir später“: Die Lücke wächst, und der nächste Agent kann die Klärung nicht wiederherstellen. Im Regelfall geschieht das schon während der Sitzung, im selben Arbeitsschritt wie die Klärung. Am Ende prüft der Agent, ob etwas liegen geblieben ist.

**Arbeitsstand nachführen.** Die Datei `devstate_active.md`, der [Arbeitsstand](../Z-anhang/Z010-glossar.md#arbeitsstand), sagt, wo das Projekt gerade steht: woran gearbeitet wird, was der nächste Schritt ist, was offen ist. Sie ist für die nächste Sitzung geschrieben und zugleich für jeden, der von außen draufschaut. Dazu zieht der Agent die [Fassaden](../Z-anhang/Z010-glossar.md#fassade) nach, die Übersichtsdateien des Wikis, damit Status und Sollzustand dort stimmen.

**Berichte ablegen.** Ergebnisse, die sich jemand später ansehen soll, etwa der Bericht eines Prüfers oder eine Recherche, kommen als Datei ins Wiki, bevor der Agent sie Ihnen im Chat zusammenfasst. Die Zusammenfassung im Chat ist flüchtig, die Datei bleibt.

**Committen.** Der Agent arbeitet mit [Git](../Z-anhang/Z010-glossar.md#git) und setzt einen [Commit](../Z-anhang/Z010-glossar.md#commit) je Zug, also je thematisch abgeschlossener Einheit. Am Ende der Sitzung folgt ein Abschluss-Commit für alles, was noch nicht erfasst ist, damit die Sitzung mit sauberem Arbeitsbaum endet. Der Arbeitsbaum sind die Dateien, die gerade in Ihrem Projektordner liegen. Sauber ist er, wenn jede Änderung daran in einem Commit steht. Ist schon alles committet, entfällt der Abschluss-Commit. Jede Commit-Nachricht beginnt mit einem Präfix aus einem festen Katalog, etwa `Wiki:` für eine Wiki-Änderung. Gepusht wird nur auf Ihre Anfrage, und Zugangsdaten gehören in keine committete Datei.

## Das macht der Agent

Die vier Schritte sind Pflicht des Agenten, nicht Ihre. Sie müssen keine Dateien schreiben. Ihr Anteil ist, das Ende anzukündigen, statt das Fenster zu schließen: „Wir hören für heute auf“ oder „Setz einen Speicherpunkt“. Das sind Beispiele, kein fester Befehl. Es genügt jede Formulierung, aus der das hervorgeht. Dann läuft die Übergabe, und der Agent meldet sie im Antwort-Raster. Hat eine Sitzung die Übergabe versäumt, fällt das beim nächsten Sessionstart auf: Zu dem, was der Agent dort prüft und meldet, gehören versäumte Übergaben.

## Beispiel DONE: mitten im Anforderungsgespräch

Sie sind mit dem Agenten im Anforderungsgespräch zu DONE. Die Frage zur Delegation aus dem vorigen Kapitel ist entschieden, die Frage zu den gelöschten Tags auch. Drei Punkte sind noch offen: die gespeicherten Sichten, die Berechnung der Fristen, der Messenger-Bot. Es ist spät. Sie schreiben: „Wir machen morgen weiter, setz einen Speicherpunkt.“

Der Agent prüft, ob beide Entscheidungen im Register stehen, und trägt nach, was fehlt. In den Arbeitsstand schreibt er: Anforderungsgespräch für den ersten Release läuft; Delegation und Tag-Löschung sind entschieden; offen sind Sichten, Fristen und Messenger-Bot, in dieser Reihenfolge; nächster Schritt ist die Frage zu den Sichten. Dann committet er, etwa mit der Nachricht `Wiki: Anforderungsgespräch DONE, Delegation und Tags entschieden`, und meldet:

```text
Erledigt:
- Entscheidungen zu Delegation und Tag-Löschung im Register.
- Arbeitsstand nachgeführt: offen sind Sichten, Fristen, Messenger-Bot.
- Abschluss-Commit gesetzt, Arbeitsbaum sauber.

Aktion (mache ich als Nächstes, sofern kein Veto):
- In der nächsten Sitzung mit den gespeicherten Sichten weitermachen.
```

Am nächsten Morgen starten Sie eine neue Sitzung. Der Agent liest den Arbeitsstand und meldet unter Aktion: Anforderungsgespräch bei den gespeicherten Sichten fortsetzen. Das Gespräch geht weiter, als wäre es nicht unterbrochen worden. Es hätte auch ein anderer Agent sein können.

## Was jetzt klar sein sollte

- Was nur im Chat steht, ist mit dem Ende der Sitzung weg. Die nächste Sitzung kennt nur Dateien.
- Vor dem Ende: Klärungen ins Wiki, Arbeitsstand nachführen, Berichte ablegen, committen.
- Das ist Pflicht des Agenten. Sie kündigen das Ende an, er stellt den Zustand her, aus dem jeder Agent übernehmen kann.
- Dieselben Schritte gelten vor jeder Übergabe, auch vor dem Start eines Subagenten.

Damit ist Teil E zu Ende. Weiter mit [Marken](../F-marken-und-freigaben/F010-marken.md): Wie der langfristige Ansatz die Arbeit schneidet, damit mehrere Dinge nebeneinander laufen können.
