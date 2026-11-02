# Wissen ins Projekt laden

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `INIT.md`, `wiki/Init-Choreografie.md`, `wiki/Konzept-Repositories.md`, `docs/Projektstart.md`; [proposals](https://github.com/schlingensiepen/proposals) `release/2026-11-02`, `README.md`, `AGENTS.md`, `agents/find-and-use.md`, `one-operation-many-surfaces/README.md`, `one-operation-many-surfaces/AGENT.md`.

Der [Startprompt](../Z-anhang/Z010-glossar.md#startprompt) sagt einmal, was das Projekt ist. Erprobte Vorgehensweisen stehen darin nicht, denn was man noch nicht kennt, kann man nicht eintippen. Neben dem Startprompt kann ein Projekt deshalb auch anders aufbereitetes Wissen laden. Dieses Kapitel zeigt den Weg am Beispiel DONE: woher das Wissen kommt, wer es auswählt und wo es danach liegt.

## Prompt und Konzept-Sammlung

Den Startprompt schreiben Sie selbst, er steht im Gespräch. Eine [Konzept-Sammlung](../Z-anhang/Z010-glossar.md#konzept-sammlung) ist anders aufgebaut. Sie bringt erprobte Vorgehensweisen in einer Form, die ein Agent gezielt nachschlägt und als Arbeitsanweisung nehmen kann. Er lädt daraus nur, was er braucht, nicht die ganze Sammlung.

Der Unterschied zum Prompt liegt an zwei Stellen. Das Wissen wird nicht eingetippt, sondern ausgewählt. Und die Kopie liegt danach im Wiki statt im Gespräch.

Das Beispiel in diesem Kapitel ist die Sammlung [`proposals`](https://github.com/schlingensiepen/proposals). Sie ist auf Englisch geschrieben, „proposal“ heißt Vorschlag. Ein einzelner Eintrag der Sammlung heißt deshalb hier Vorschlag.

## Der Weg in vier Schritten

Das Laden läuft beim [Einrichten](../Z-anhang/Z010-glossar.md#init) von selbst, wie im Kapitel [Ein Projekt aufsetzen](D035-ein-projekt-aufsetzen.md) beschrieben. Das Regelwerk nennt diesen Abschnitt Konzept-Angebot. Für DONE sieht er so aus:

1. **Der Referenzprozess bringt die Sammlung mit.** Zum [Referenzprozess](../Z-anhang/Z010-glossar.md#referenzprozess) gehört ein [Register](../Z-anhang/Z010-glossar.md#register) der Sammlungen, darin steht `proposals`. Der Startprompt für DONE nennt die Sammlung deshalb nicht.
2. **Der Agent sichtet und markiert.** Beim Einrichten sichtet er nur die Übersicht der Sammlung, in der Regel durch einen [Subagenten](../Z-anhang/Z010-glossar.md#subagent), einen Hilfs-Agenten mit eigenem, frischem Kontext. Je Vorschlag markiert er, ob er für Ihr Projekt empfohlen, neutral oder nicht relevant ist. „Keine Empfehlung“ ist dabei ein gültiges Ergebnis.
3. **Sie wählen aus.** Nichts ist Pflicht. Sie nehmen einzelne Vorschläge, sagen „später“, dann kommt das Angebot nach dem [Mission Statement](../Z-anhang/Z010-glossar.md#mission-statement) noch einmal, oder Sie übernehmen nichts.
4. **Der Agent übernimmt das Gewählte.** Für jeden gewählten Vorschlag bucht er eine [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) und legt eine Kopie ins Wiki, mit Herkunft und Datum. Dann schlägt er Einträge in den Registern vor. Sie entstehen erst, wenn Sie sie bestätigt haben.

![Links stehen untereinander die Blöcke Startprompt und Konzept-Sammlung, zwischen ihnen gibt es keinen Pfeil. Von beiden führt je ein Pfeil zum Block Agent. Vom Agenten führt ein Pfeil Vorschlag zum Block Sie, von dort ein Pfeil Auswahl zurück. Vom Agenten führt ein Pfeil Übernahme in einen grauen Container Projekt mit den Blöcken Entscheidung, Kopie im Wiki und Einträge in Registern.](bilder/D050-wissen-laden.svg)

**Zwei Wege ins Projekt.** Der Startprompt beschreibt das Projekt, die Sammlung bringt der Referenzprozess mit. Ins Projekt kommt nur, was Sie aus dem Vorschlag des Agenten auswählen.

Im Projekt liegt danach mehr als ein Text: eine Entscheidung, wie Sie sie im Kapitel [Register und Elemente](D040-register-und-elemente.md) kennengelernt haben, und daneben die Kopie mit ihrer Herkunft.

## Ein Vorschlag als Beispiel

Ein Vorschlag aus `proposals` heißt `one-operation-many-surfaces`. Seine Kernaussage: Jede Handlung gibt es genau einmal, alle Zugänge reichen nur durch. Das passt zum Backend von DONE, auf dem alle Zugänge aufsetzen: Mobile-App, Desktop-App, Kommandozeilen-Werkzeug, MCP-Server und Messenger-Bot. Ein TODO anzulegen gäbe es dann an genau einer Stelle, und kein Zugang baut diese Handlung für sich noch einmal nach. Das ist nur ein Beispiel, die Empfehlung Ihres Agenten kann anders ausfallen.

## Einordnung

- Die Vorschläge in `proposals` haben den Status Entwurf, und der Agent sagt Ihnen das dazu. Die Sammlung stellt sie zur Diskussion, als bewährt gelten sie damit noch nicht.
- Wo mehrere Antworten richtig sind, entscheiden Sie. Der Agent legt Ihnen die Möglichkeiten vor, statt still eine zu wählen.
- Eine Sammlung ist austauschbar. Das Register der Sammlungen gehört dem Projekt, und eine weitere Sammlung lässt sich beim Einrichten oder später nennen.

## Was jetzt klar sein sollte

- Der Startprompt sagt einmal, was das Projekt ist. Eine Konzept-Sammlung bringt Vorgehensweisen, die ein Agent gezielt nachschlägt und als Arbeitsanweisung nehmen kann.
- Dieses Wissen wird nicht eingetippt, sondern ausgewählt. Die Kopie liegt danach im Wiki statt im Gespräch.
- Die Sammlung kommt über das Register des Referenzprozesses ins Spiel, nicht über den Startprompt.
- Der Agent sichtet und markiert, Sie wählen aus, nichts ist Pflicht. Für jedes Gewählte entstehen eine Entscheidung und eine Kopie mit Herkunft, Einträge in den Registern erst nach Ihrer Bestätigung.

Weiter mit [Wer entscheidet was](../E-mensch-und-agent/E010-wer-entscheidet-was.md): welche Entscheidungen der Agent selbst trifft und welche nur Sie treffen können.
