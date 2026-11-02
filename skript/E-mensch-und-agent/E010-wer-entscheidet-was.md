# Wer entscheidet was

> **Stand der Quellen:** [referenzprozess-softwareentwicklung](https://github.com/schlingensiepen/referenzprozess-softwareentwicklung) `release-2.0`, `docs/Arbeitsweise.md`.

Im Kapitel [Anforderungen im Gespräch](../B-der-naive-ansatz/B010-anforderungen-im-gespraech.md) galt eine einfache Regel: Der Agent fragt, der Mensch entscheidet. So einfach bleibt es nicht, denn der Agent soll Sie nicht mit jeder Kleinigkeit aufhalten. Was darf er allein tun, was legt er Ihnen vor, und was fragt er? Dieses Kapitel zieht diese Grenze. Es zeigt die drei Arbeitsmodi, in denen ein Agent nach dem Regelwerk arbeitet, und die feste Form seiner Meldungen, an der Sie im Betrieb sehen, wer gerade entscheidet.

## Ableiten oder entscheiden

Die Grundregel heißt: Ableitbarkeit vor Rückfrage. Bevor der Agent eine Frage stellt, prüft er, ob die Antwort schon in den Dateien des Projekts steht. Steht sie dort, leitet er sie ab und legt Ihnen das Ergebnis als Entwurf vor. Sie bestätigen oder korrigieren. Gefragt wird nur, was sich nicht ableiten lässt: Ihr [Bearbeiter-Kürzel](../Z-anhang/Z010-glossar.md#bearbeiter-kürzel), eine Auswahl unter gleichwertigen Möglichkeiten, Stolpersteine aus Ihrer Erfahrung.

Nehmen Sie das Beispiel DONE. Der [Startprompt](../Y-beispiele/Y020-done-mit-referenzprozess.md) nennt ein Backend und fünf Zugänge darauf: Mobile-App, Desktop-App, Kommandozeile, einen Server für Agenten und einen Messenger-Bot. Welche Ordner das Projekt für diese Zugänge braucht, folgt aus der Liste. Das leitet der Agent ab, legt die Struktur als Entwurf vor und wartet nicht auf eine Antwort je Ordner. Ob die Mobile-App schon zum ersten Release gehört oder erst später kommt, steht dagegen nirgends. Das ist Funktionsumfang, und den entscheiden Sie.

Drei Dinge bleiben immer bei Ihnen, auch wenn der Agent sie ableiten könnte: inhaltliche Festlegungen, die als [Entscheidung](../Z-anhang/Z010-glossar.md#entscheidung) ins Register gehören; Ihr eigenes Terrain im [Wiki](../Z-anhang/Z010-glossar.md#wiki), die Datei `wiki/Facts.md` und das Glossar; und alles, was nach außen wirkt oder Geld kostet, etwa ein Versand oder die Installation eines Werkzeugs. Dort legt der Agent einen Entwurf vor und wartet.

## Die drei Arbeitsmodi

Das Regelwerk unterscheidet drei Modi. Sie unterscheiden sich darin, was der Agent bei einer Unklarheit tut.

**Standard-Modus.** Das ist die Grundeinstellung, der [Standard-Modus](../Z-anhang/Z010-glossar.md#standard-modus). Bei Unklarheit fragt der Agent nach und führt nicht aus. Das gilt besonders für inhaltliche Entscheidungen, für Formulierungen in Dokumenten, die nach außen gehen, und für alles mit Außenwirkung. Im Zweifel fragt er also, statt etwas anzunehmen.

**Standardaufgaben.** Manche Vorgänge sind so festgelegt, dass es nichts zu entscheiden gibt: einen Commit setzen, den Index des Wikis pflegen, das Protokoll führen, ein eingegangenes Dokument als Wiki-Knoten anlegen, nach einer Installation die Datei `Tools.md` nachführen, den Bericht eines Subagenten ins Wiki übernehmen. Solche [Standardaufgaben](../Z-anhang/Z010-glossar.md#standardaufgabe) führt der Agent ohne Rückfrage aus. Er meldet jeden Schritt sichtbar, und Sie können ihn per Veto zurücknehmen lassen. Das ist keine Erlaubnis, spontan zu handeln: Die Befreiung von der Rückfrage gilt nur für die Folgeschritte einer Aufgabe, die schon ausgelöst ist. Wird innerhalb einer Standardaufgabe etwas unklar, fällt der Agent in den Standard-Modus zurück und fragt.

**Arbeitsmodus.** Bei großen Mengen, etwa wenn beim Start eines Projekts dreißig Dokumente eingelesen werden, würde eine Rückfrage bei jeder Unklarheit Sie den ganzen Tag beschäftigen. Dafür schlägt der Agent den [Arbeitsmodus](../Z-anhang/Z010-glossar.md#arbeitsmodus) vor; er gilt nur mit Ihrer Zustimmung. Darin fragt er nicht, sondern schreibt jede Unklarheit in die Datei `Offene Fragen.md`: den Zusammenhang, die Frage, was er übersprungen hat und was nachzuarbeiten ist. Den betroffenen Teilschritt lässt er aus und arbeitet am nächsten weiter. Am Ende legt er Ihnen die gesammelten Fragen vor. Nur bei einer kritischen Unklarheit, wenn ohne Klärung große Teile des Ergebnisses falsch würden, verlässt er den Modus von selbst.

Verwechseln Sie die Arbeitsmodi nicht mit der [Berechtigungsstufe](../Z-anhang/Z010-glossar.md#berechtigungsstufe) aus [Die erste Sitzung](../A-verstehen-und-loslegen/A040-die-erste-sitzung.md). Die Berechtigungsstufe ist eine Einstellung des Agenten: Sie legt fest, was er technisch ohne Ihr OK tun kann, etwa Dateien ändern. Die Arbeitsmodi sind Regeln des Regelwerks: Sie legen fest, wann der Agent fragt, bevor er etwas tut, auch wenn er es technisch dürfte.

## Woran Sie es im Betrieb sehen

Wer gerade entscheidet, lesen Sie an der Form der Meldungen ab. Strukturierte Meldungen des Agenten, etwa beim Sessionstart, bei einer Zusammenfassung oder an einem Übergabepunkt, haben immer dieselben drei Blöcke, das [Antwort-Raster](../Z-anhang/Z010-glossar.md#antwort-raster):

```text
Erledigt:
- …

Aktion (mache ich als Nächstes, sofern kein Veto):
- …

Frage (brauche ich von dir):
- …
```

Unter **Erledigt** steht, was der Agent getan oder festgestellt hat, eine reine Statusmeldung. Auch Ergebnisse von Prüfungen stehen hier, auch rote. Sie werden berichtet, nicht zur Blockade der Arbeit gemacht; über die Weiterarbeit entscheiden Sie. Unter **Aktion** steht, was der Agent als Nächstes tut, wenn Sie nicht widersprechen. Hier landet alles Ableitbare, als Entwurf. Lesen Sie diesen Block aufmerksam, denn Schweigen heißt Zustimmung. Unter **Frage** steht nur, was der Agent wirklich von Ihnen braucht. Im laufenden Betrieb sind das höchstens ein bis zwei Fragen je Meldung.

Die Blöcke werden nicht vermischt: Eine Frage steht nie im Aktion-Block, ein Entwurf nie im Frage-Block. Interne Nummern des Regelwerks nennt der Agent Ihnen gegenüber nicht, Sie sehen nur die Substanz.

Im Beispiel DONE könnte eine Meldung kurz nach dem Einrichten so aussehen:

```text
Erledigt:
- Projekt nach der Anleitung eingerichtet, erste Marke 1.0 angelegt.

Aktion (mache ich als Nächstes, sofern kein Veto):
- Mission Statement aus dem Startprompt als Entwurf ablegen.
- Für das Backend und die fünf Zugänge je einen Ordner anlegen.

Frage (brauche ich von dir):
- Gehört die Mobile-App schon zum ersten Release oder erst zu einem späteren?
```

Die Ordner sind ableitbar, also Aktion. Der Umfang des ersten Release ist es nicht, also Frage.

## Was jetzt klar sein sollte

- Der Agent leitet ab, was aus den Dateien folgt, und legt es als Entwurf vor. Er fragt nur, was sich nicht ableiten lässt.
- Inhaltliche Festlegungen, Ihr Terrain im Wiki und alles mit Außenwirkung bleiben bei Ihnen.
- Drei Modi: Im Standard-Modus fragt er bei Unklarheit. Standardaufgaben führt er ohne Rückfrage aus und meldet sie. Im Arbeitsmodus sammelt er Fragen in einer Datei, nur mit Ihrer Zustimmung.
- Das Antwort-Raster Erledigt, Aktion, Frage zeigt, wer entscheidet. Was unter Aktion steht, tut er als Nächstes, wenn Sie nicht widersprechen.

Weiter mit [Entscheiden im Gespräch](E020-entscheiden-im-gespraech.md): Wie der Agent Ihnen die Entscheidungen vorlegt, die bei Ihnen liegen.
