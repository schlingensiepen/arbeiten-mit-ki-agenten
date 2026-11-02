# Werkstatt, Produkt, Schleuse

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Mehrere-Repos.md`, `wiki/Two-Repo-Submodul-Muster.md`.

Beim Aufsetzen eines Projekts stellt der Agent eine Frage, die im Kapitel [Ein Projekt aufsetzen](../D-wissen-im-wiki/D035-ein-projekt-aufsetzen.md) nur kurz vorkam: ein Repo mit allem oder ein zweites Repo für das Produkt? Für DONE fiel die Antwort auf ein Repo. Dieses Kapitel erklärt die andere Antwort. Sie löst ein Problem, das jedes Projekt irgendwann hat: Die Arbeit soll privat bleiben, das Ergebnis soll nach außen. Im Wiki stehen Entscheidungen, verworfene Wege, Notizen aus den Sitzungen, Prüfberichte. Das ist wertvoll, aber nicht für Außenstehende bestimmt. Der Code und sein Handbuch sollen dagegen öffentlich sein, mit einer Geschichte, die man vorzeigen kann.

## Zwei Repos

Die Lösung sind zwei [Repos](../Z-anhang/Z010-glossar.md#repo) mit verschiedenen Rollen. Das eine ist das Arbeits-Repo: Dort liegt das [Wiki](../Z-anhang/Z010-glossar.md#wiki) mit seinen Registern, dort stehen die Freigabedokumente, dort ist die ganze Historie. Das Regelwerk nennt es die [Werkstatt](../Z-anhang/Z010-glossar.md#werkstatt). Das andere ist das Repo, das das Produkt der Marke trägt, bei Software den Code, die Tests und den Build, also alles, was aus dem Code ein lauffähiges Programm macht. Das Regelwerk nennt es das Produkt-Repo, und dort setzt der Agent den Git-Tag aus dem Kapitel [Softwareentwicklung als Prozess](G010-softwareentwicklung-als-prozess.md). Dazu kommen im Produkt-Repo die Dokumente, die Menschen außerhalb des Projekts lesen, etwa eine Betriebs-Anleitung.

Zwei Dinge sind dabei leicht zu verwechseln. Erstens: Code wird nicht aus dem Wiki abgeleitet. Er entsteht direkt im Produkt-Repo, und was dabei festgelegt wird, bucht der Agent im Wiki. Abgeleitet werden nur die Dokumente. Zweitens: Nur eines der drei Wörter im Titel setzt zwei Repos voraus. Das [Produkt](../Z-anhang/Z010-glossar.md#produkt) gibt es in jedem Projekt, auch mit einem Repo; es ist das, was der Git-Tag markiert. Die Werkstatt gibt es in diesem Skript ebenfalls immer: Sie ist der Ort der Arbeit mit Wiki, Registern und Historie, so haben Sie das Wort in Teil C kennengelernt. Bei einem Repo liegt sie mit dem Produkt im selben Repo. Die Schleuse gibt es erst bei zwei Repos, denn erst dann gibt es eine Grenze, über die etwas geregelt hinübergeht. Das Regelwerk selbst ist hier enger: Es benutzt auch das Wort Werkstatt nur für zwei Repos und sagt bei einem Repo einfach Wiki.

## Kleinteilig diesseits, vollständig jenseits

Das Wiki ist für den Agenten gebaut. Es besteht aus kleinen Knoten, die aufeinander verweisen, und aus Registern mit nummerierten Elementen. Der Agent liest nur, was er braucht, und folgt den Links. Ein Freigabedokument verweist auf seine Elemente, statt sie zu kopieren. Das Regelwerk nennt solche Dokumente wiki-verweisend: Sie sind nur mit dem Wiki lesbar.

Ein Leser außerhalb des Projekts hat das Wiki nicht. Für ihn muss ein Dokument in sich vollständig sein: keine Links ins Wiki, keine Register-Nummern, jede Begründung ausgeschrieben. Das Regelwerk nennt das [selbsttragend](../Z-anhang/Z010-glossar.md#selbsttragend). Das Handbuch für die Benutzer von DONE ist so ein Dokument.

Der Übergang von der einen Form in die andere ist keine Kopie und kein Export. Ein selbsttragendes Dokument wird aus dem Wiki vollständig neu erzeugt, jedes Mal. Es wird nie nachgepflegt. Der Grund: Die Wahrheit liegt im Wiki, und nur dort. Würde jemand im Handbuch einen Satz korrigieren, gäbe es zwei Fassungen der Wahrheit, und die nächste Ableitung würde die Korrektur überschreiben. Stattdessen wird im Wiki korrigiert und das Handbuch neu erzeugt.

## Die Schleuse

Den geregelten Übergang von der Werkstatt ins Produkt nennt das Regelwerk die [Schleuse](../Z-anhang/Z010-glossar.md#schleuse). Sie ist kein Programm, sondern eine Regel, die der Agent als Knoten im Wiki anlegt und mit Ihnen in sieben Feldern klärt. Für jedes Feld legt er eine Vorgabe vor, die Sie ändern können:

1. **Quelle:** Welcher Teil der Werkstatt ist die Wahrheit? Vorgabe: das Wiki, die Register und die Freigabedokumente.
2. **Ziel:** Welches Repo, welcher Ordner wird abgeleitet? Vorgabe: das Produkt-Repo, die Dokumente für Menschen etwa in einem Ordner für den Betrieb.
3. **Auslöser:** Wann wird abgeleitet? Vorgabe: die Freigabe eines Freigabedokuments für das Ausliefern, oder Ihr Zuruf.
4. **Transformation:** Was fließt wie von der Quelle ins Ziel? Vorgabe: vollständige Neu-Erzeugung, aus wiki-verweisend wird selbsttragend.
5. **Ausschlüsse:** Was darf nicht ins Ziel? Interna, Verweise in die Werkstatt, Vermerke an Entwürfen.
6. **Freigabe:** Wer gibt die Ableitung frei? Vorgabe: nach einem Review wie im vorigen Kapitel. Ob der Agent danach selbst ableitet und Sie ein Veto haben oder ob Sie jede Ableitung vorab freigeben, legen Sie in diesem Feld fest. Beim Übertrag ins Produkt bietet der Agent das Review von sich aus an, in verschärfter Form.
7. **Rück-Sync-Verbot:** Das Ziel wird nie in die Quelle zurückgespielt. Änderungen laufen immer über die Werkstatt.

Dazu kommt eine Regel für den Fall, dass mehrere Beteiligte an den Repos arbeiten, Mensch und Agent oder mehrere Agenten: Jedes Repo gehört genau einem Bearbeiter, der dort ohne Ankündigung schreiben darf. In jedes andere Repo wird nur mit vorheriger Ankündigung geschrieben.

![Links ein grauer Container Werkstatt mit drei blauen Blöcken: Wiki, Knoten verlinkt; Register, nummerierte Elemente; Freigabedokumente, eingefroren. Darunter steht: ganze Historie, bleibt privat. Rechts ein grauer Container Produkt mit einem blauen Block Code und Tests, entstehen hier, und einem gelben Block Handbuch, in sich vollständig. Darunter steht: vorzeigbare Historie. Zwischen den Containern ein oranger Block Schleuse, neu erzeugt; ein schwarzer Pfeil führt von den Freigabedokumenten in die Schleuse, ein oranger Pfeil von der Schleuse zum Handbuch. Oben führt ein gestrichelter grauer Pfeil vom Code zurück zur Werkstatt, beschriftet: nie zurück.](bilder/G030-zwei-repos.svg)

**Zwei Repos und der Übergang.** Die Werkstatt hält Wiki, Register und Freigabedokumente mit der ganzen Historie. Im Produkt entsteht der Code direkt; das Handbuch wird durch die Schleuse aus den Freigabedokumenten neu erzeugt. Aus dem Produkt fließt nichts zurück.

## Wie die zwei Repos zusammenhängen

Technisch liegt das Produkt-Repo als Submodul im Arbeits-Repo, also als eigenes Repo in einem Unterordner, wenn die Werkzeuge das hergeben. Sonst liegen zwei Repos nebeneinander, und eine Ignorier-Regel sorgt dafür, dass das eine das andere nicht mit aufnimmt. Für das Remote, also den Ort im Netz, bietet der Agent die Dienste an, die er kennt, etwa [GitHub](../Z-anhang/Z010-glossar.md#github), und legt es nach Ihrer Zustimmung an.

Bei einem Repo gelten dieselben Regeln ohne die Grenze: Selbsttragende Dokumente liegen dann in einem Ordner desselben Repos und werden zu denselben Anlässen vollständig neu erzeugt. Nur Submodul und Schleusen-Regel entfallen. Das Muster ist außerdem rekursiv: Ein Produkt-Repo kann selbst wieder Werkstatt für ein eigenes Teil-Produkt sein.

## Beispiel: DONE mit zwei Repos

Stellen Sie sich vor, DONE soll veröffentlicht werden, die Arbeit daran nicht. Die Werkstatt ist das Repo, das Sie kennen: das Wiki mit den Anforderungen, den Entscheidungen, den Freigabedokumenten der Marke 1.0 und den Prüfberichten aus dem vorigen Kapitel. Das Produkt ist ein zweites Repo mit dem Backend, der Kommandozeile und den Tests; dort steht der Git-Tag der Marke 1.0. Dazu liegt dort das Handbuch: wie man DONE installiert, wie man ein TODO anlegt, delegiert und in Sichten findet. Der Agent hat es aus dem Wiki erzeugt, als die Beschreibung der Auslieferung für die Marke 1.0 freigegeben war, und Sie haben es nach einem Review freigegeben.

Nun meldet ein Benutzer, dass im Handbuch ein Befehl der Kommandozeile falsch steht. Der Fehler wird nicht im Handbuch korrigiert. Er wird im Wiki behoben, dort, wo die Funktion beschrieben ist, und das Handbuch wird neu erzeugt und erneut freigegeben. Das Produkt-Repo zeigt danach genau eine saubere Änderung: Handbuch zur Marke 1.0, zweite Fassung. Die Diskussion, wie der Fehler entstand, bleibt in der Werkstatt.

## Was jetzt klar sein sollte

- Zwei Repos trennen Arbeit und Ergebnis: Die Werkstatt hält Wiki, Register und Historie und bleibt privat; das Produkt-Repo hält Code, Tests und die Dokumente für Menschen und kann öffentlich sein.
- Das Wiki ist kleinteilig und verlinkt, für den Agenten. Was nach außen geht, ist selbsttragend: ohne Links ins Wiki, ohne Nummern, mit ausgeschriebenen Begründungen.
- Die Schleuse ist eine Regel in sieben Feldern. Ihr Kern: vollständige Neu-Erzeugung statt Nachpflegen, Freigabe nach Review, und nichts fließt zurück.
- Code wird nicht abgeleitet. Er entsteht im Produkt-Repo; seine Festlegungen werden im Wiki gebucht.

Weiter mit [Bestehende Projekte](G040-bestehende-projekte.md): Was geschieht, wenn ein Projekt schon da ist, bevor das Regelwerk kommt.
