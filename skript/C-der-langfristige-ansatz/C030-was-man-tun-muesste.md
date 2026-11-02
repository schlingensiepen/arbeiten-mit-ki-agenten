# Was man tun müsste

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Staende-Freigaben-Marken.md`.

Das vorige Kapitel hat sieben Forderungen aufgestellt und zu jeder in der mittleren Spalte einen Ansatz genannt. Dieses Kapitel nimmt die sechs Ansätze einzeln vor. Es zeigt noch nicht, wie die Vorlage sie umsetzt, das tun die Teile D bis H. Es zeigt den Gedanken hinter jedem Ansatz: Stellen Sie sich vor, Sie hätten nur die Forderungen in der Hand und müssten die Arbeitsweise selbst entwerfen. Was müssten Sie tun? Wer die sechs Antworten kennt, erkennt in den folgenden Teilen jedes Werkzeug als Antwort auf eine Frage, die hier gestellt wurde, und das ist der Zweck des Kapitels: Es ist das letzte, das begründet. Danach wird gebaut.

## Wissen auslagern

Die ersten beiden Forderungen lauteten: Wissen übersteht die Sitzung, und der Agent liest nur, was er braucht. Was man dafür tun müsste, hat zwei Hälften, und die zweite ist die schwierigere.

Die erste Hälfte: Alles, was eine Sitzung überdauern soll, kommt aus dem Chat heraus und in Dateien hinein. Nicht nur die Anforderungen, die lagen in der Dokumentenkette auch schon auf der Platte. Auch die Regeln, nach denen gearbeitet wird, die Entscheidungen, die gefallen sind, und der Punkt, an dem die Arbeit gerade steht. Wenn das alles in Dateien liegt, muss es niemand mehr am Anfang einer Sitzung erklären. Die Sitzung beginnt leer, aber nicht ahnungslos: Der Agent liest zu Beginn, was für ihn bereitliegt.

Die zweite Hälfte: Eine einzige Datei, die alles enthält, ist nur eine größere Ausgabe des Problems aus dem Kapitel [Warum der naive Ansatz scheitert](C010-warum-der-naive-ansatz-scheitert.md). Sie wächst, bis sie nicht mehr in den Kontext passt. Also muss das Wissen in viele kleine Dateien zerfallen, die aufeinander verweisen, und an jedem Verweis muss stehen, was dahinter wartet. Dann liest der Agent den Einstieg, folgt den Verweisen, die seine Aufgabe betreffen, und lässt die übrigen liegen. Das ist ein [Wiki](../Z-anhang/Z010-glossar.md#wiki): die Sammlung verlinkter Dateien im Projekt, die als Quelle der Wahrheit für Wissen und Festlegungen gilt. Was dort steht, gilt; was nur im Chat gesagt wurde, gilt nicht, bis es dort steht.

Das ist Teil D. Das Kapitel [Das Wiki](../D-wissen-im-wiki/D010-das-wiki.md) zeigt die Struktur, das Kapitel [Regelwerk und Sessionstart](../D-wissen-im-wiki/D020-regelwerk-und-sessionstart.md) zeigt, wie der Agent am Anfang jeder Sitzung findet, was er braucht.

## Entscheidungen beim Menschen

Die dritte Forderung: Entscheidungen sind nachvollziehbar und bleiben beim Menschen. Was man dafür tun müsste, ist ebenfalls zweierlei.

Erstens braucht es einen Ort, an dem jede Entscheidung steht. Nicht im Datenmodell versteckt, wie beim Storno in Teil B, sondern ausgeschrieben: was gewählt wurde und warum. Jede [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) bekommt eine Nummer und kommt in ein [Register](../Z-anhang/Z010-glossar.md#register), eine Übersichtsdatei mit nummerierten Einträgen. Ist sie dort, wird sie nicht mehr umgeschrieben. Wer anders entscheiden will, trifft eine neue Entscheidung, die die alte ablöst, und die alte bleibt lesbar stehen. So kann eine spätere Sitzung nachvollziehen, nicht nur was gilt, sondern auch, was vorher galt und warum es sich geändert hat.

Zweitens braucht es eine klare Rollenverteilung im Gespräch. Die Vorlage zieht die Linie so: Was sich mechanisch prüfen lässt, etwa ob Tests grün sind, darf der Agent selbst feststellen und auf Wunsch auch selbst buchen. Was ein Urteil verlangt, bleibt Prüfern oder Personen vorbehalten. Stößt der Agent auf eine Lücke, etwa eine Grundlage, die fehlt oder noch nicht freigegeben ist, dann warnt er, nennt die Optionen und blockiert nicht. Entschieden wird von Ihnen. Der Agent bereitet vor, schlägt vor, führt aus und schreibt auf. Auch eine Freigabe ist in der Vorlage eine Entscheidung, die als Eintrag im Register steht.

Das Register zeigt das Kapitel [Register und Elemente](../D-wissen-im-wiki/D040-register-und-elemente.md). Wie das Gespräch aussieht, in dem der Agent vorlegt und Sie wählen, ist Teil E, beginnend mit [Wer entscheidet was](../E-mensch-und-agent/E010-wer-entscheidet-was.md).

## Nach Marken schneiden statt nach Schritten

Die vierte Forderung: Änderungen laufen nicht durch alles. Hier liegt die eigentliche Wende gegenüber Teil B, und sie betrifft die Frage, wonach die Arbeit geordnet wird.

Die Dokumentenkette ordnete nach Schritten: ein Dokument je Schritt, von vorn nach hinten. Sobald es eine zweite Version gab, brauchte sie eine zweite Kette, und ab da liefen zwei Wahrheiten nebeneinander. Was man tun müsste, ist, die Schnittlinie zu drehen. Die Einheit, nach der geordnet wird, ist nicht der Schritt, sondern das Ergebnis, das nach außen geht: Version 1.0, Version 1.1. Die Vorlage nennt ein solches Ergebnis eine [Marke](../Z-anhang/Z010-glossar.md#marke): ein benanntes Ergebnis, das nach außen geht und freigegeben wird, kein Datum. Von außen sieht man von einem Projekt seine Marken und deren Produkte; nach innen ordnen die Marken alles Übrige.

Daraus folgt, wie eine Änderung aussieht. Jedes [Element](../Z-anhang/Z010-glossar.md#element), etwa eine Anforderung, trägt die Marke, zu der es gehört. Was für eine Marke feststeht, wird eingefroren: Aus dem lebenden Wissen des Wikis entsteht ein [Freigabedokument](../Z-anhang/Z010-glossar.md#freigabedokument), das zu genau einer Marke gehört. Kommt für Version 1.1 eine Änderung, ist sie ein neues Element ab dieser Marke. Das alte Element gilt für Version 1.0 weiter, das neue ab 1.1. Nichts wird kopiert, nichts wird umgeschrieben; es gibt eine Fassung je Marke, und jede sagt, wofür sie gilt. Damit ist die Ursache der parallelen Wahrheiten beseitigt, nicht nur ihr Symptom.

Die Schritte verschwinden dabei nicht. Sie bleiben als Angebot, als Liste dessen, woran zu denken ist: Der Agent fragt, ob Sie etwas schon bedacht haben, und Sie antworten, wo es steht, dass es übersprungen wird oder dass Sie es jetzt tun. Was die Schritte dann noch ordnen, ist das Thema des nächsten Ansatzes. Die Marken selbst sind Teil F, beginnend mit dem Kapitel [Marken](../F-marken-und-freigaben/F010-marken.md).

## Arbeit parallelisierbar machen

Die fünfte Forderung: Arbeit läuft nebeneinander. In der Kette war das verboten, weil jedes Dokument das vorige voraussetzte. Was man tun müsste, ist, Reihenfolge nur dort zu verlangen, wo sie etwas garantiert.

Die Vorlage sagt: Die Schritte ordnen Freigaben, nicht Arbeit. Ein Eintrag darf jederzeit entstehen und angenommen werden, sobald man ihn weiß, eine Anforderung also auch beim Testen, eine Entscheidung zur Technik auch vor der Architektur. Geordnet ist allein, in welcher Reihenfolge die Freigabedokumente freigegeben werden. Gearbeitet wird fließend und parallel; gesperrt wird die Arbeit nie.

Dafür müssen zwei Voraussetzungen stimmen. Die Einheiten der Arbeit müssen klein sein und sich nicht gegenseitig überschreiben: Ein Element wird nicht geändert, sondern abgelöst, und zwei Leute, die je ein neues Element anlegen, kommen sich nicht ins Gehege, anders als zwei, die dasselbe Dokument bearbeiten. Und was man jemandem zum Weiterarbeiten übergibt, muss stillhalten: Die Vorlage nennt als einen Zweck eines Freigabedokuments ausdrücklich den Auftrag an einen weiteren Agenten. Ein eingefrorenes Dokument kann man übergeben, ein lebendes nicht.

Die erste Hälfte, Arbeit in beliebiger Reihenfolge, löst Teil F. Die zweite Hälfte, mehrere Agenten, die nebeneinander arbeiten, ist Teil H, beginnend mit dem Kapitel [Subagenten](../H-mehrere-agenten/H010-subagenten.md).

## Prüfen lassen

Die sechste Forderung: Jemand prüft unabhängig. Was man dafür tun müsste, ist, Bauen und Prüfen zu trennen und der Prüfung einen Gegenstand, einen Maßstab und ein Ergebnis zu geben.

Der Gegenstand ist das eingefrorene Freigabedokument, nicht das lebende Wiki, denn nur was stillhält, lässt sich prüfen. Der Maßstab sind die Vorgänger, die schon freigegeben sind. Die Vorlage prüft ein Dokument vor seiner Freigabe gegen alle freigegebenen Vorgänger derselben Marke auf drei Dinge: Widerspruch, also ob es einem Vorgänger widerspricht; Abdeckung, also ob alles aus den Vorgängern aufgegriffen ist; und Unbegründetes, also Inhalt, den kein Vorgänger trägt. Das Ergebnis ist ein Prüfbericht, auf den die Freigabe verweist.

Unabhängig heißt dabei zweierlei: ein eigener Kontext, der die Missverständnisse des Bauens nicht teilt, und nach Möglichkeit ein anderes Modell als das, das gebaut hat. War es dasselbe Modell, steht das als Einschränkung ausdrücklich bei der Freigabe. Und die Prüfung sperrt nicht: Die Arbeit läuft weiter, nur die Freigabe setzt die Prüfung voraus. Darin unterscheidet sich der zweite Blick von einem Wächter, der alles anhält.

Das ist Teil G. Das Kapitel [Softwareentwicklung als Prozess](../G-der-gesamtprozess/G010-softwareentwicklung-als-prozess.md) zeigt die Folge der Freigabedokumente, in der jedes gegen seine Vorgänger geprüft wird, das Kapitel [Prüfen](../G-der-gesamtprozess/G020-pruefen.md) zeigt, wie Agenten diese Prüfung übernehmen.

## Das Produkt vom Arbeitsmaterial trennen

Die siebte Forderung: Arbeitsmaterial und Ergebnis sind getrennt. Was man dafür tun müsste, beginnt mit einer Festlegung und endet mit einer Regel.

Die Festlegung: Was ist das [Produkt](../Z-anhang/Z010-glossar.md#produkt)? Bei Software der Quelltext in bestimmten Ordnern, in anderen Projekten etwa ein Text. Welche Pfade dazugehören, legt das Projekt fest, und das Produkt wird nicht als Dokument freigegeben, sondern mit einer Markierung im Versionsverlauf, die sagt, welcher Zustand der freigegebene ist. Alles andere, das Wiki, die Register, die Freigabedokumente und die Historie, ist die [Werkstatt](../Z-anhang/Z010-glossar.md#werkstatt): der Ort, an dem gearbeitet wird und aus dem das Produkt hervorgeht.

Die Regel: Was nach außen geht, entsteht aus der Werkstatt, nicht von Hand. Die Dokumente der Werkstatt verweisen aufeinander, mit Nummern und Links, und sind nur mit dem Wiki vollständig lesbar. Für Empfänger ohne Zugang entstehen daraus Ableitungen, die für sich allein stehen: ohne Verweise ins Wiki, ohne Registernummern, mit ausgeschriebenen Begründungen. Sie werden zu festen Anlässen vollständig neu erzeugt und nie nachgebessert, und sie tragen einen Kopf, der sagt, woraus sie stammen. Die Zeile „Stand der Quellen“ über diesem Kapitel ist genau so ein Kopf: Dieses Skript ist eine solche Ableitung. Den geregelten Übergang von der Werkstatt ins Produkt nennt das Skript [Schleuse](../Z-anhang/Z010-glossar.md#schleuse).

Das Kapitel [Werkstatt, Produkt, Schleuse](../G-der-gesamtprozess/G030-werkstatt-produkt-schleuse.md) führt das aus.

## Die Teile D bis H als Antwort

Die sechs Ansätze sind zugleich der Fahrplan für den Rest des Skripts. Ab Teil D begleitet Sie dafür das zweite Beispiel, die Aufgabenverwaltung DONE.

| Ansatz | Teil | Erstes Kapitel |
|---|---|---|
| Wissen auslagern | D Wissen im Wiki | [Das Wiki](../D-wissen-im-wiki/D010-das-wiki.md) |
| Entscheidungen beim Menschen | E Mensch und Agent | [Wer entscheidet was](../E-mensch-und-agent/E010-wer-entscheidet-was.md) |
| Nach Marken schneiden | F Marken und Freigaben | [Marken](../F-marken-und-freigaben/F010-marken.md) |
| Parallelisierbar machen | F, dazu H Mehrere Agenten | [Subagenten](../H-mehrere-agenten/H010-subagenten.md) |
| Prüfen lassen, Produkt trennen | G Der Gesamtprozess | [Softwareentwicklung als Prozess](../G-der-gesamtprozess/G010-softwareentwicklung-als-prozess.md) |

## Was jetzt klar sein sollte

- Wissen auslagern heißt: aus dem Chat in viele kleine, verlinkte Dateien, an jedem Link ein Hinweis, was dahinter wartet. Was dort steht, gilt.
- Entscheidungen beim Menschen heißt: jede Entscheidung mit Nummer und Begründung im Register, abgelöst statt umgeschrieben; der Agent legt vor und warnt, Sie wählen.
- Nach Marken schneiden heißt: geordnet wird nach dem Ergebnis, das nach außen geht, nicht nach dem Arbeitsschritt. Eine Änderung ist ein neues Element ab einer Marke, das alte gilt für frühere Marken weiter.
- Parallelisierbar machen heißt: Reihenfolge nur bei den Freigaben, nie bei der Arbeit. Eingefrorene Dokumente lassen sich übergeben, auch an weitere Agenten.
- Prüfen lassen heißt: eigener Kontext, möglichst anderes Modell, drei Fragen an das eingefrorene Dokument, ein Bericht, und die Arbeit wird nie gesperrt.
- Das Produkt trennen heißt: festlegen, was das Produkt ist, und alles Übrige als Werkstatt behandeln, aus der Ableitungen vollständig neu erzeugt werden.

Weiter mit [Das Wiki](../D-wissen-im-wiki/D010-das-wiki.md): der erste Ansatz, Wissen auslagern, und wie ein Wiki im Projektordner aussieht.
