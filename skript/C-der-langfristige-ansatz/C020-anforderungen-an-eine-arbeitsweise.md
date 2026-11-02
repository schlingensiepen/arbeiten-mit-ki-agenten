# Anforderungen an eine Arbeitsweise

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Staende-Freigaben-Marken.md`.

In Teil B haben Sie für die Lagerverwaltung erst die Anforderungen entwickelt und dann gebaut. Dasselbe tut dieses Kapitel für die Arbeitsweise selbst. Das vorige Kapitel hat sechs Ursachen benannt, an denen der naive Ansatz scheitert. Aus ihnen folgen sieben Forderungen an eine Arbeitsweise, die langfristig trägt, also über Wochen, über viele Sitzungen und über mehrere Versionen. Die Tabelle nennt zu jeder Forderung schon den Ansatz, den das nächste Kapitel ausführt, und den Teil des Skripts, der ihn einlöst. Das ist ein Vorgriff; was die Wörter in der mittleren Spalte bedeuten, kommt noch.

| Forderung | Ansatz | Teil |
|---|---|---|
| 1. Wissen übersteht die Sitzung | Wissen auslagern | D |
| 2. Der Agent liest nur, was er braucht | Wissen auslagern | D |
| 3. Entscheidungen sind nachvollziehbar und bleiben beim Menschen | Entscheidungen beim Menschen | E, dazu D |
| 4. Änderungen laufen nicht durch alles | nach Marken schneiden | F |
| 5. Arbeit läuft nebeneinander | parallelisierbar machen | F, H |
| 6. Jemand prüft unabhängig | prüfen lassen | G |
| 7. Arbeitsmaterial und Ergebnis sind getrennt | Produkt vom Arbeitsmaterial trennen | G |

## 1. Wissen übersteht die Sitzung

Der Kontext ist Arbeitsspeicher. Endet die Sitzung, ist er weg, und mit ihm alles, was nur im Gespräch stand. Die Dokumentenkette hatte dafür schon eine halbe Antwort: Die Dokumente lagen auf der Platte. Gefehlt hat alles andere, die Regeln, die Entscheidungen, der Stand der Arbeit. Die Forderung: Alles, was eine Sitzung überdauern soll, liegt als Datei im Projekt, und die nächste Sitzung findet es dort.

Die Antwort darauf ist ein [Wiki](../Z-anhang/Z010-glossar.md#wiki) im Projektordner, Teil D. Die Vorlage sagt dazu, lebendes Wissen ändere sich dort fortlaufend, und genau das ist gewollt: Das Wiki ist der Ort, an dem das Wissen lebt, nicht der Chat.

## 2. Der Agent liest nur, was er braucht

Die zweite Forderung folgt aus der Kontextgrenze und widerspricht der ersten nur scheinbar. Wenn alles auf der Platte liegt, liegt dort bald sehr viel, und der Agent darf es nicht alles lesen. Also muss das Wissen so abgelegt sein, dass er findet, was er für die Aufgabe braucht, und den Rest liegen lässt. Das ist eine Forderung an die Struktur: verlinkte Dateien, bei denen an jedem Link steht, was dahinter wartet.

Auch das löst Teil D. Beide Forderungen zusammen heißen: Wissen auslagern, und zwar so, dass es sich stückweise lesen lässt.

## 3. Entscheidungen sind nachvollziehbar und bleiben beim Menschen

Im Fall mit dem Storno wurde entschieden, nichts zu löschen. Diese Entscheidung stand nirgends, sie steckte im Datenmodell. Eine Sitzung später weiß niemand mehr, ob das Absicht war. Die Forderung hat zwei Hälften. Erstens: Jede Entscheidung wird aufgeschrieben, mit dem, was gewählt wurde, und warum. Zweitens: Entscheidungen trifft der Mensch. Der Agent schlägt vor, legt vor, führt aus, aber ob gelöscht oder deaktiviert wird, sagen Sie.

Die Vorlage hält das durchgängig so. Wo eine Prüfung ein Urteil verlangt, bleibt es Prüfern oder Personen vorbehalten; der Agent fragt, und Sie entscheiden. Jede [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) kommt mit Nummer, Wahl und Begründung in ein Register und wird nur noch durch eine neue Entscheidung abgelöst. Wie das Gespräch dabei aussieht, zeigt Teil E, das Register zeigt das Kapitel [Register und Elemente](../D-wissen-im-wiki/D040-register-und-elemente.md).

## 4. Änderungen laufen nicht durch alles

Das war der Bruch in Teil B: Eine Änderung berührte jedes Dokument hinter ihr, und bei zwei Versionen jedes Dokument zweimal. Die Forderung: Eine Änderung erzeugt etwas Neues, statt Bestehendes umzuschreiben, und sie betrifft nur das, wofür sie gilt.

Die Vorlage tut dafür zweierlei. Sie schneidet die Arbeit nicht nach Schritten, sondern nach [Marken](../Z-anhang/Z010-glossar.md#marke): benannten Ergebnissen, die nach außen gehen, etwa Version 1.0 und Version 1.1. Und sie friert ein, worauf sich jemand verlassen soll: Aus dem lebenden Wissen wird ein eingefrorenes [Freigabedokument](../Z-anhang/Z010-glossar.md#freigabedokument) zu genau einer Marke. Ändert sich danach etwas, entsteht ein neues Dokument, das alte bleibt unverändert liegen. Ein Element, das ein älteres ablöst, gilt ab seiner Marke; für die Marken davor gilt das alte weiter. So gibt es keine Kopien, die auseinanderlaufen, sondern Fassungen, von denen jede sagt, wofür sie gilt. Das ist Teil F.

## 5. Arbeit läuft nebeneinander

Die starre Reihenfolge der Kette verbot, an Version 2 zu arbeiten, während Version 1 noch lief, und sie verbot, beim Testen eine Anforderung nachzutragen. Die Forderung: Die Arbeitsweise erlaubt, in beliebiger Reihenfolge und an mehreren Stellen zugleich zu arbeiten, ohne dass die Verlässlichkeit verloren geht.

Die Vorlage formuliert es so: Die Schritte ordnen Freigaben, nicht Arbeit. Ein Eintrag darf jederzeit entstehen und angenommen werden, sobald man ihn weiß; geordnet ist allein, in welcher Reihenfolge die Freigabedokumente freigegeben werden. Gearbeitet wird fließend und parallel. Das macht die Arbeit in Teil F parallelisierbar, und Teil H nimmt dann weitere Agenten hinzu, die nebeneinander arbeiten.

## 6. Jemand prüft unabhängig

Grün heißt nicht richtig, das war das Ende von Teil B. Die Forderung: Bevor sich jemand auf ein Ergebnis verlässt, prüft es jemand, der nicht mitgeschrieben hat, mit eigenem Kontext und möglichst mit einem anderen Modell. Und die Prüfung sperrt die Arbeit nicht, sie ist Voraussetzung dafür, dass man sich verlassen darf.

Genau so hält es die Vorlage: Vor der Freigabe wird ein Dokument gegen seine Vorgänger geprüft, auf Widerspruch, auf Abdeckung und auf Unbegründetes, durch einen Prüfer mit einem anderen Modell als dem, das gebaut hat. Die Arbeit wird dabei nie gesperrt; nur die Freigabe setzt die Prüfung voraus. Das Kapitel [Prüfen](../G-der-gesamtprozess/G020-pruefen.md) zeigt, wie das mit Agenten geht.

## 7. Arbeitsmaterial und Ergebnis sind getrennt

Am Ende von Teil B lag im Projektordner alles durcheinander. Die Forderung: Was man weitergibt, ist von dem getrennt, womit man arbeitet, und es entsteht aus dem Arbeitsmaterial nach einer festen Regel, nicht von Hand.

Die Vorlage nennt den Ort der Arbeit [Werkstatt](../Z-anhang/Z010-glossar.md#werkstatt) und das Weitergegebene Produkt. Für Empfänger ohne Zugang zur Werkstatt entstehen aus den Freigabedokumenten Ableitungen, die für sich allein lesbar sind: vollständig neu erzeugt, nicht nachgepflegt, mit einem Kopf, der sagt, woraus sie stammen. Dieses Skript ist selbst so entstanden. Wie der Übergang von der Werkstatt ins Produkt geregelt ist, zeigt das Kapitel [Werkstatt, Produkt, Schleuse](../G-der-gesamtprozess/G030-werkstatt-produkt-schleuse.md).

## Was jetzt klar sein sollte

- Eine Arbeitsweise, die trägt, muss sieben Dinge leisten, und jede Forderung folgt aus einer Ursache des vorigen Kapitels.
- Zwei Forderungen betreffen das Wissen: Es überlebt die Sitzung, und es lässt sich stückweise lesen.
- Eine betrifft die Entscheidungen: aufgeschrieben, begründet, vom Menschen getroffen.
- Zwei betreffen die Änderungen: Sie laufen nicht durch alles, und Arbeit läuft nebeneinander.
- Zwei betreffen das Ergebnis: Es wird unabhängig geprüft, und es ist vom Arbeitsmaterial getrennt.

Weiter mit [Was man tun müsste](C030-was-man-tun-muesste.md): die Ansätze aus der mittleren Spalte, bevor die Teile D bis H sie einlösen.
