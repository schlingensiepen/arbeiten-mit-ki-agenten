# Das Wiki

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Einfuehrung.md`, `docs/Wiki-und-Register.md`, `Wiki.md`, `MasterPrompt.md`.

> **Ein Agent muss nicht alles lesen. Er hangelt sich durch, wie in der Wikipedia.**

Im Kapitel [Was man tun müsste](../C-der-langfristige-ansatz/C030-was-man-tun-muesste.md) stand als erste Forderung: Das Wissen muss aus dem Gespräch heraus und auf die Platte. Dieses Kapitel zeigt die Form, die das Wissen dort bekommt. Sie heißt [Wiki](../Z-anhang/Z010-glossar.md#wiki): ein Ordner `wiki/` im Projekt, voller kleiner Textdateien, die aufeinander verweisen. Das Wiki ist nicht aus Ordnungsliebe da, sondern aus einem technischen Grund, den Sie schon kennen: Das Fenster des Modells ist begrenzt. Wer den Grund versteht, versteht auch, warum der Agent beim Lesen so sparsam ist, und warum das richtig so ist.

## Warum ein Wiki: das begrenzte Fenster

Erinnern Sie sich an das Kapitel [Kontext](../A-verstehen-und-loslegen/A020-kontext.md). Alles, was dem Modell bei einer Antwort vorliegt, muss in das [Kontextfenster](../Z-anhang/Z010-glossar.md#kontextfenster) passen, und das ist begrenzt. Die laufende Unterhaltung ist deshalb Arbeitsspeicher, keine Quelle. Wird sie lang, verdichtet der Agent sie und verliert Einzelheiten. Endet die [Sitzung](../Z-anhang/Z010-glossar.md#sitzung), ist sie weg. Wer am nächsten Tag weiterarbeitet, ob derselbe Agent, ein anderer Agent oder Sie selbst, muss alles, was gilt, allein durch Lesen der Dateien wiederherstellen können. Das Regelwerk fasst das in einen Satz: Wissen lebt auf der Platte, nicht im Kopf.

Im naiven Ansatz lag das Wissen über die Lagerverwaltung in einer Kette von Dateien: `anforderungen.md`, `datenmodell-und-ablaeufe.md`, `spezifikation.md`. Das hat einen Haken: Durchlesen heißt immer, eine ganze Datei in den Kontext zu laden, und um zu wissen, was gilt, braucht der Agent alle. Werden die Dateien größer, wird jedes Lesen teurer. Legt man für jede Version weitere Dateien an, muss der Agent trotzdem vieles neu erklärt bekommen, und welche davon gilt, steht nirgends. Die Lösung ist, das Wissen in viele kleine Dateien zu zerlegen, die so verlinkt sind, dass man immer nur das Stück lesen muss, das man gerade braucht.

Das Bild dafür ist die Wikipedia. Niemand liest sie ganz. Man steigt bei einem Artikel ein, und an jedem Link steht, was dahinter wartet. Man folgt nur den Links, die zur eigenen Frage gehören. Technisch ist das Wiki genau das, nur auf der Festplatte: Textdateien, nach einer festen Regel miteinander verlinkt. Ein Beispiel: Wer wissen will, wie das Auslagern in der Lagerverwaltung ablaufen soll, muss nicht alle Anforderungen lesen, vom Einlagern bis zur Auswertung. Eine Seite genügt, und die findet man über Links.

Die Dateien sind Markdown: Text mit Überschriften, Listen und Tabellen, lesbar mit jedem Editor. Ein eigenes Programm für das Wiki brauchen Sie nicht.

## Quelle der Wahrheit

Im Wiki liegt alles projektspezifische Wissen: Fakten, Begriffe, Anforderungen, Entscheidungen, Fehlermeldungen, die Architektur, wie weit die Arbeit ist. Das Wiki ist die Quelle der Wahrheit des Projekts. Das Regelwerk formuliert es als Grundgesetz: Was nicht im Wiki steht, ist nicht festgelegt. Daraus folgen für den Agenten zwei Pflichten.

- **Lese-Pflicht.** Vor jeder Behauptung über eine Festlegung und vor jeder Frage an Sie schlägt der Agent im Wiki nach. Behauptet er eine Festlegung, nennt er die Nummer des Eintrags. Ohne Nummer ist es eine Erinnerung, und Erinnerungen werden erst geprüft, dann ausgesprochen.
- **Pflege-Pflicht.** Was Sie mit dem Agenten im Gespräch klären, wandert im selben Arbeitsschritt in eine Datei. Nicht „das machen wir später“: Die Lücke wächst, und der nächste Agent kann die Klärung nicht wiederherstellen.

Ein Beispiel aus der Lagerverwaltung: Sie klären im Gespräch, dass ein Artikel immer genau einem Lagerort zugeordnet ist. Beim naiven Ansatz steht das jetzt im Chat und ist morgen vergessen. Mit Wiki legt der Agent es sofort als Eintrag ab, mit Nummer und Begründung, und jede spätere Antwort zur Lagerverwaltung kann sich darauf stützen. Wie solche Einträge aussehen, zeigt das Kapitel [Register und Elemente](D040-register-und-elemente.md).

> **Das Wissen gehört nicht nur in den Chat, sondern in die Dateien im Projektordner. Und die gehören Ihnen.**

Das ist die zweite Seite derselben Sache. Die Dateien liegen in Ihrem Ordner, in Ihrem Format, und Sie dürfen selbst hineinschreiben. Fehlt etwas, tragen Sie es ein und reden mit dem Agenten weiter darüber. Nichts davon ist in einem Dienst eingesperrt.

## Aufbau: Fassaden und Detail-Knoten

Damit das Wiki trotz seines Umfangs lesbar bleibt, ist es in zwei Ebenen gebaut.

- **Fassaden** sind Übersichtsdateien, am Stück lesbar, je Thema genau eine: die Projektfakten, die Anforderungen, die Entscheidungen, die Marken, das Glossar. Jede [Fassade](../Z-anhang/Z010-glossar.md#fassade) beschreibt in einem eigenen Abschnitt `Meta` selbst, wozu sie da ist und wie sie gepflegt wird.
- **Detail-Knoten** sind einzelne Dateien je Wissensobjekt: eine Anforderung, eine Entscheidung mit ihrer Begründung, ein eingegangenes Dokument, ein Fachbegriff.

Die Fassade verweist auf ihre Detail-Knoten. Beim Start einer Sitzung lädt der Agent die wichtigsten Fassaden vollständig, die übrigen merkt er sich nur. Den Verweisen in die Detail-Knoten folgt er erst, wenn er Einzelheiten braucht. Verweise sind Wikilinks, ein Dateiname in doppelten eckigen Klammern. Der Ordner ist flach, die Dateinamen sind lesbar, Umlaute werden umschrieben.

Der entscheidende Kunstgriff steht an den Links selbst. Wissen, das an mehreren Stellen gebraucht wird, steht an genau einem Ort, und von überall sonst wird dorthin verlinkt. Wo ein Link steht, steht kurz dabei, was hinter ihm zu erwarten ist: der Gegenstand, der Zweck, der Moment, in dem man ihn lesen sollte. Etwa: „Anforderungen: welche Buchungen die Lagerverwaltung kennt, zu lesen vor jeder Funktionsbeschreibung.“ Ohne diese Beschreibung müsste der Agent jedes Ziel ganz lesen, um zu wissen, ob er es braucht. Mit ihr liest er nur, was sein Auftrag verlangt. Das Regelwerk nennt das Kontextökonomie, und es ist der eigentliche Zweck der Verlinkung. Ordnung ist nur die Nebenwirkung.

![Links ein grüner Block Auftrag mit dem Text Auslagern beschreiben. Rechts ein grauer Container wiki mit einer blauen Fassade Anforderungen, die drei beschriftete Verweise enthält: Einlagern, Auslagern, Report. Von den Verweisen führen Pfeile zu drei blauen Detail-Knoten. Orange hervorgehoben ist der Weg vom Auftrag in die Fassade, von dort zum Knoten Auslagern und weiter in einen gelben Block Kontext, der Auftrag, Fassade und einen Detail-Knoten enthält. Die beiden anderen Verweise bleiben schwarz.](bilder/D010-lesepfad.svg)

**Der Lesepfad.** Der Agent liest die Fassade, folgt nur dem Verweis, den sein Auftrag braucht, und in seinem Kontext liegen am Ende der Auftrag, die Fassade und ein einziger Detail-Knoten.

So lässt sich das Wiki auch verstehen: Es ist ein Weg, einen Agenten mit einem bestimmten Auftrag durch das Wissen und die Festlegungen eines Projekts zu schicken. Er liest den Einstieg, erkennt an den Beschreibungen, welche Türen für seinen Auftrag die richtigen sind, und lässt die anderen zu. Was er nicht liest, kostet keinen Platz im Fenster.

## Das Wiki kommt nicht leer

Sie bauen kein Wiki, Sie füllen eines. Der Referenzprozess, mit dem im Kapitel [Ein Projekt aufsetzen](D035-ein-projekt-aufsetzen.md) ein Projekt beginnt, liefert ein vorbereitetes `wiki/` mit: alle Fassaden als Skelette, dazu die Regeln, nach denen der Agent sie pflegt. Zwei Hilfsdateien führt der Agent automatisch, einen Index aller Detail-Knoten und ein Protokoll aller Übernahmen; die bearbeiten Sie nicht.

Das Wiki ist dabei nur einer von mehreren Ordnern mit fester Rolle. Originale, die Sie hereingeben, etwa PDF-Dateien, liegen in `raw/` und werden nie verändert. Ihre Umwandlung in Text, den der Agent lesen kann, liegt in `input/` und bleibt ebenso unverändert. Das Wiki lebt und ändert sich ständig. Was eingefroren und freigegeben wird, liegt in `output/`; darum geht es im Teil [Marken und Freigaben](../F-marken-und-freigaben/README.md).

## Was jetzt klar sein sollte

- Das Wiki folgt aus dem begrenzten Kontextfenster: Die Unterhaltung ist Arbeitsspeicher, die Dateien sind die Quelle. Was nicht im Wiki steht, ist nicht festgelegt.
- Der Agent schlägt vor jeder Behauptung nach und legt jede Klärung sofort ab.
- Fassaden geben den Überblick, Detail-Knoten die Einzelheiten. An jedem Link steht, was dahinter wartet, deshalb liest der Agent nur, was sein Auftrag braucht.
- Die Dateien sind Markdown im Projektordner, und sie gehören Ihnen.

Weiter mit [Regelwerk und Sessionstart](D020-regelwerk-und-sessionstart.md): woher der Agent weiß, wie er arbeiten soll, was er beim Start liest und wie eine Sitzung abläuft.
