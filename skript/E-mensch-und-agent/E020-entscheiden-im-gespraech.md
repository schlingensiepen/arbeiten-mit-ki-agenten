# Entscheiden im Gespräch

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Arbeitsweise.md` und `wiki/templates/Styleguide-chat-Vorlage.md`.

Im vorigen Kapitel haben Sie gesehen, welche Entscheidungen bei Ihnen bleiben. In einem Projekt sind das viele, und sie kommen selten einzeln. Im Beispiel DONE wirft allein das Anforderungsgespräch ein Dutzend Fachfragen auf. Wer sie in der Reihenfolge beantwortet, in der sie dem Agenten einfallen, verliert den Überblick und entscheidet am Ende Dinge, die sich längst erledigt hatten. Dieses Kapitel zeigt, wie der Agent Klärpunkte nach dem Regelwerk vorlegt: in welcher Reihenfolge, in welcher Form, und wie Sie das Gespräch steuern.

## Zuerst die Frage, die am meisten festlegt

Bleiben mehrere Fragen, ordnet der Agent sie nicht nach ihrem Auftreten, sondern nach ihrer Wirkung: Zuerst kommt die Frage, deren Antwort am meisten anderes mitentscheidet. Nach jeder Antwort prüft er, welche Folgefragen sich damit erledigt haben oder nun ableitbar sind, und stellt sie nicht mehr.

Ein Beispiel aus DONE. Der Startprompt legt fest, dass sich Aufgaben, dort TODOs genannt, an andere Benutzer delegieren lassen und beide Seiten eine eigene, verlinkte Aufgabe behalten. Daraus ergeben sich offene Punkte: Gilt die Aufgabe des Auftraggebers als erledigt, wenn der Empfänger seine erledigt? Darf der Empfänger weiterdelegieren? Welche Tags trägt die Aufgabe beim Empfänger? Die erste Frage kommt zuerst. Hängen die beiden Aufgaben im Status zusammen, liegt nahe, dass auch Fristen und Sichten zusammenhängen, und mehrere Folgefragen beantworten sich von selbst. Ist die Aufgabe beim Empfänger dagegen eigenständig, stellen sich die Fragen zu Tags und Fristen neu.

## Erst der Fahrplan, dann die Kette

Führt der Agent Sie durch zwei oder mehr zusammenhängende Entscheidungen, zeigt er vorher einen Fahrplan: welche Entscheidungen anstehen, in welcher Reihenfolge, was wovon abhängt und was er aufzuschieben vorschlägt. Der Fahrplan enthält keine Optionen und keine Empfehlungen, nur die Übersicht. Erst nach Ihrer Rückmeldung beginnt die erste Einzelfrage. Der Grund: Wer eine Kette von Entscheidungen durchläuft, deren Ende er nicht kennt, entscheidet nicht wirklich frei.

## Briefing-Modus

Stehen etwa drei oder mehr Klärpunkte an, zeigt der Agent zuerst die Liste, je Punkt eine Zeile, geordnet wie oben. Dazu bietet er den [Briefing-Modus](../Z-anhang/Z010-glossar.md#briefing-modus) an: Je Punkt gibt er ein kurzes Briefing, also Sachlage und Zusammenhang, schlägt einen oder mehrere Lösungswege vor, Sie diskutieren und entscheiden, und weiter geht es erst, wenn Sie „weiter“ sagen. Fachbegriffe erklärt er im Briefing kurz. Sie sollen auf Grundlage der Vorschläge entscheiden können, ohne selbst nachlesen zu müssen. Die Alternative ist, alle Punkte im Block zu klären. Sie können jederzeit wechseln, etwa mit „den Rest im Block“. Wollen Sie es dauerhaft so, bucht der Agent die Vorliebe als Regel des Projekts ins Wiki.

## Auswahlmenüs

Ist eine Entscheidung eine Wahl zwischen zwei bis vier klaren Möglichkeiten, bekommen Sie kein Für und Wider im Fließtext, sondern ein nummeriertes [Auswahlmenü](../Z-anhang/Z010-glossar.md#auswahlmenü). Jeder Punkt trägt eine kurze Erläuterung, was er bedeutet und welche Folgen die Wahl hat; nackte Optionen ohne Zusammenhang gibt es nicht. Sie antworten mit einer Ziffer oder einem Wort. Eine eigene Antwort außerhalb des Menüs ist immer möglich.

So könnte das im Anforderungsgespräch zu DONE aussehen. Der Startprompt sagt: Tags lösen die Kategorien der Methode ab, und was keinen Tag hat, liegt in der Inbox. Der Agent stößt auf eine Lücke:

```text
Offener Punkt: Ein Tag wird gelöscht, an dem noch TODOs hängen.

1. Die TODOs verlieren den Tag. Was danach keinen Tag mehr hat,
   liegt in der Inbox. Folgt der Regel aus dem Startprompt, kann
   die Inbox aber unerwartet voll werden.
2. Der Tag lässt sich nicht löschen, solange TODOs ihn tragen.
   Nichts rutscht unbemerkt in die Inbox, dafür muss man vor dem
   Löschen alle TODOs umhängen.
3. Der Tag wird nur ausgeblendet. Die TODOs behalten ihn, in
   Sichten und Filtern taucht er nicht mehr auf. Nichts geht
   verloren, aber es gibt zwei Arten von Tags.

Vorschlag: 1, weil die Regel aus dem Startprompt dann ohne
Ausnahme gilt.
```

Sie antworten „1“. Ab jetzt ist das eine [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) des Projekts mit Nummer und Begründung, wie Sie es aus [Register und Elemente](../D-wissen-im-wiki/D040-register-und-elemente.md) kennen. Dass sie auch dort ankommt und nicht im Chat liegen bleibt, ist Thema des nächsten Kapitels.

## Widerspruch und Lob

Zwei Regeln für den Ton. Erstens: Der Agent lobt Ihre Vorschläge nicht. „Hervorragende Idee“ und „genau richtig“ sagen nichts über die Sache; eine kurze Bestätigung reicht, und sachliche Rückfragen bleiben erlaubt. Zweitens: Widersprechen Sie dem Agenten, prüft er kurz, was für ein Widerspruch das ist. Ist es eine Vorliebe, folgt er ihr ohne Diskussion. Kollidiert Ihre Anweisung mit einer Regel des Regelwerks, weist er sachlich darauf hin und fragt, ob die Regel geändert werden soll; er ändert sie nicht stillschweigend. Kollidiert sie mit einer früheren Anweisung von Ihnen, auch aus einer früheren Sitzung, macht er den Widerspruch sichtbar und fragt, welche gilt, bevor er handelt.

Das klingt nach Kleinigkeiten, ist aber der Kern des Gesprächs: Sie entscheiden, der Agent sorgt dafür, dass Sie mit vollständiger Sicht entscheiden, und keine Regel ändert sich, nur weil jemand widersprochen hat.

## Was jetzt klar sein sollte

- Fragen kommen in der Reihenfolge ihrer Wirkung: zuerst die, die am meisten anderes festlegt. Erledigte Folgefragen entfallen.
- Vor einer Kette von Entscheidungen steht ein Fahrplan ohne Optionen.
- Ab etwa drei Klärpunkten bietet der Agent den Briefing-Modus an: je Punkt Sachlage, Vorschläge, Ihre Entscheidung, weiter auf Zuruf.
- Einfache Entscheidungen kommen als Auswahlmenü mit Erläuterung je Option; eine eigene Antwort bleibt möglich.
- Kein Lob, kein stilles Nachgeben: Bei einem Widerspruch klärt der Agent, ob eine Vorliebe, eine Regel oder eine frühere Anweisung betroffen ist.

Weiter mit [Eine Sitzung sauber beenden](E030-eine-sitzung-sauber-beenden.md): Was aus dem Gespräch in die Dateien muss, bevor die Sitzung endet.
