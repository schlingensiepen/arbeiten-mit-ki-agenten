# Einen Agenten bekommen

> **Stand der Quellen:** [clawbook-lehre](https://github.com/schlingensiepen/clawbook-lehre) `main`, `docs/README.md`, `docs/installation.md`, `docs/setup/README.md`, `docs/pflege.md`.

Die ersten beiden Kapitel haben erklärt, was ein Agent ist und warum sein Kontext begrenzt ist. Jetzt brauchen Sie einen. Dieses Kapitel zeigt die drei Wege dorthin, beschreibt einen davon Schritt für Schritt und gibt Ihnen die wenigen Befehle mit, die Sie im Terminal brauchen. Alles Weitere in diesem Skript setzt voraus, dass bei Ihnen ein Agent läuft.

## Drei Wege

Ein Agent besteht aus einem Harness auf Ihrem Rechner und einem Modell beim Anbieter. Sie brauchen also beides: ein Programm und einen Zugang. Dafür gibt es drei Wege.

1. **Selbst installieren.** Sie installieren den Harness eines Anbieters auf Ihrem eigenen Rechner, etwa Claude Code, Codex oder Copilot CLI, und melden ihn mit Ihrem Konto an. Das ist der allgemeine Weg. Er setzt voraus, dass Sie auf dem Rechner Software installieren dürfen und sich um Git, Python, Node.js und die übrigen Werkzeuge selbst kümmern.
2. **Den der Firma benutzen.** In vielen Unternehmen und Hochschulen ist ein Agent vorgegeben, samt Zugang und Regeln. Dann richten Sie nichts ein, arbeiten aber mit dem, was gestellt wird.
3. **clawbook.** [clawbook](../Z-anhang/Z010-glossar.md#clawbook) ist ein fertig eingerichteter Arbeitsrechner für die Arbeit mit KI-Agenten, verpackt als Container-Image, das sich unter Windows ohne Administrator-Rechte starten lässt. Git, Python, Node.js und mehrere Agenten sind darin schon installiert und aufeinander abgestimmt.

Dieses Skript zeigt den dritten Weg, weil er mit einem Befehl zu einem vollständigen Arbeitsplatz führt und weil alle im Kurs dann dieselbe Ausstattung haben. Die Arbeitsweise, die die folgenden Kapitel beschreiben, hängt nicht daran. Wer einen eigenen oder einen gestellten Agenten hat, überspringt die Einrichtung und liest ab dem Abschnitt über die ersten Befehle weiter.

Eines gilt auf jedem Weg: Agenten und die Modelle dahinter sind nicht gleich. Modelle haben je nach Aufgabe unterschiedliche Stärken, etwa beim Schreiben von Dokumentation oder beim Prüfen von Code, und die Rangfolge ändert sich mit jeder neuen Version. Legen Sie sich nicht auf ein Werkzeug fest, weil es das erste war. Was im Kurs verbindlich ist, sagt Ihnen die Kursleitung.

## Was clawbook ist

Drei Wörter braucht man, um den Aufbau zu verstehen. Ein [Terminal](../Z-anhang/Z010-glossar.md#terminal) ist ein Fenster, in das Sie Befehle tippen; darin läuft eine [Shell](../Z-anhang/Z010-glossar.md#shell), das Programm, das die Befehle entgegennimmt und ausführt. Ein [Container](../Z-anhang/Z010-glossar.md#container) ist eine abgeschlossene Umgebung auf einem Rechner, die ihre eigene Software mitbringt und vom Rest weitgehend getrennt ist, hier ein kompletter Linux-Rechner, den Windows wie ein Programm startet und anhält. [WSL](../Z-anhang/Z010-glossar.md#wsl), das Windows-Subsystem für Linux, ist der Teil von Windows, mit dem Linux-Programme unter Windows laufen; er verwaltet den Container.

![Ein großer Container Windows, Ihr Rechner. Links darin drei grüne Blöcke: PowerShell, VS Code und Browser. Rechts darin eine Fläche WSL, in der ein orange beschrifteter Container clawbook liegt, mit den Blöcken Agenten und Werkzeuge, darunter claude, codex, copilot, agy, git, und Home-Volume mit Projekten und Anmeldungen. Pfeile führen von PowerShell mit ssh clawbook und von VS Code mit Remote-SSH in den Container. Außerhalb von Windows stehen rechts die Blöcke Sprachmodell beim Anbieter, erreicht vom Container mit Prompt und Antwort, und Konten der Anbieter, erreicht vom Browser mit Anmeldung.](bilder/A030-aufbau-clawbook.svg)

**Windows, WSL, Container und Zugänge.** Der Container ist ein eigener Linux-Rechner in WSL. Sie erreichen ihn aus PowerShell und aus VS Code, die Agenten darin sprechen mit den Modellen der Anbieter, und Ihre Anmeldungen bei den Anbietern laufen im Browser unter Windows.

Warum Linux? Agenten laufen zunehmend in Unix-artigen Umgebungen, und die Befehle eines Linux-Terminals passen zu ihnen, wie im Kapitel [Was ein Agent ist](A010-was-ein-agent-ist.md) beschrieben: Text hinein, Text heraus. Ihre Projekte und Ihre Anmeldungen liegen in einem eigenen Speicherbereich, dem Home-Volume. Er überlebt neue Versionen des Images und lässt sich als eine Datei auf einen anderen Rechner mitnehmen.

Ein Container ist ein eigener Rechner, und das hat eine Grenze: Geräte, die an Ihrem Windows hängen, etwa ein Mikrocontroller am USB-Anschluss, sieht er nicht. Wer Hardware programmiert, braucht dafür weiterhin ein Programm unter Windows (Stand Oktober 2026).

## Einrichten in vier Schritten

Die vollständige Anleitung mit allen Fehlerfällen steht im Repository von clawbook. Hier steht der Weg, damit Sie wissen, was auf Sie zukommt. Planen Sie für den ersten Durchlauf etwa eine Stunde ein; das meiste davon ist Wartezeit beim Herunterladen. Nehmen Sie dafür eine stabile Internetverbindung, nicht das WLAN im Zug.

**1. Voraussetzungen prüfen.** Sie brauchen Windows 10 oder 11 mit WSL ab Version 3.0.1, den OpenSSH-Client von Windows und etwa 20 GB freien Platz. Öffnen Sie PowerShell, das Terminal von Windows, und prüfen Sie:

```powershell
wsl --version
ssh -V
```

Ist WSL zu alt, hilft `wsl --update`, auch ohne Administrator-Rechte. Fehlt WSL ganz, steht in der Anleitung, wie Sie es auf dem eigenen Rechner einrichten; auf einem Hochschulrechner fragen Sie die Betreuung.

**2. Der eine Befehl.** In PowerShell einfügen und ausführen:

```powershell
irm https://raw.githubusercontent.com/schlingensiepen/clawbook-lehre/main/get-clawbook.ps1 | iex
```

Der Befehl lädt ein Verwaltungs-Skript und zeigt ein Menü. Beim ersten Mal wählen Sie „neu einrichten“. Dann lädt das Skript das Image, legt das Home-Volume und den Container an und richtet SSH ein. Lassen Sie das Fenster offen und brechen Sie nicht ab. Am Ende steht ein grüner Kasten „clawbook läuft“. Derselbe Befehl dient später zum Starten, Aktualisieren und Sichern; das Menü ändert sich dann.

**3. Verbinden im Terminal.** In einem neuen PowerShell-Fenster:

```powershell
ssh clawbook
```

SSH ist das Verfahren, mit dem Sie sich von Windows aus im Container anmelden; statt eines Passworts dient eine Schlüsseldatei, die das Skript angelegt hat. Beim ersten Verbinden fragt der Container, ob Sie sich bei [GitHub](../Z-anhang/Z010-glossar.md#github) anmelden wollen. GitHub ist ein Dienst im Netz, auf dem Projekte liegen; Sie brauchen ein kostenloses Konto. Melden Sie sich gleich an, denn Git und der Projektverwalter des Containers bauen darauf auf. Beantragen Sie bei der Gelegenheit das Student Developer Pack von GitHub: Die Prüfung dauert einige Tage, und mit ihm ist der Agent Copilot CLI für Studierende kostenlos.

Danach erscheint das clawbook-Menü. Mit `0` schließen Sie es und landen in der Eingabezeile des Containers. Sie erkennen sie daran, dass die Zeile mit `student@` beginnt und nicht mehr mit `PS C:\`. Alles, was Sie jetzt tippen, läuft im Container. Mit `exit` kommen Sie zurück nach Windows, der Container läuft weiter.

**4. Verbinden mit VS Code.** Für die tägliche Arbeit nehmen Sie VS Code, den Editor. Führen Sie den Befehl aus Schritt 2 erneut aus und wählen Sie Menüpunkt 9. Beim ersten Mal richtet das Skript ein eigenes VS Code für clawbook ein, danach startet es VS Code und verbindet es mit dem Container. VS Code ist dabei nur das Guckloch: Der Editor läuft unter Windows, Dateien, Terminal und Git liegen im Container. Dass die Verbindung steht, sehen Sie unten links an „SSH: clawbook“. Auf die Frage, ob Sie den Autoren der Dateien in diesem Ordner vertrauen, antworten Sie mit Ja. Es ist Ihr eigener Ordner.

Ein Terminal im Container öffnen Sie in VS Code über das Menü „Terminal → New Terminal“. Zwei Stolperstellen: Wer oben in die Leiste klickt, landet in der Suche; die Befehlspalette, in der Sie Befehle wie „Create New Terminal (With Profile)“ eingeben, erreichen Sie mit F1. Und VS Code startet zunächst auf Englisch.

Einen grafischen Bildschirm hat der Container auch, erreichbar über die Remotedesktopverbindung von Windows. Sie brauchen ihn selten, etwa für eine Anmeldung, die nur im Browser des Containers funktioniert. Die Anleitung beschreibt den Weg.

## Zugänge anmelden

Im Container sind die Werkzeuge installiert, aber noch nicht angemeldet. Die Zugänge gehören Ihnen, deshalb stecken sie nicht im Image. Sie richten sie einmal ein; sie landen in Ihrem Home-Verzeichnis und bleiben erhalten.

Welche Agenten im Container liegen und was sie kosten, steht in der Übersicht der Anleitung, mit Datum, weil sich Preise und Angebote ändern. Zum Stand Oktober 2026 sind es Claude Code (`claude`), Codex (`codex`), Copilot CLI (`copilot`), OpenCode (`opencode`) und Antigravity (`agy`). Sie müssen nichts kaufen, um anzufangen: Für jedes Werkzeug gibt es einen kostenlosen Einstieg, und die Anleitung nennt die Reihenfolge, in der Sie vorgehen. Wenn Sie etwas Kostenpflichtiges abschließen, gilt überall dasselbe: Abos verlängern sich automatisch, also das Kündigungsdatum in den Kalender; bei Guthaben nach Verbrauch das automatische Nachladen ausschalten und ein Ausgabenlimit setzen.

Die Anmeldung läuft bei fast allen Werkzeugen gleich. Sie starten das Werkzeug im Container, es zeigt einen Link und einen Code, Sie öffnen den Link im Browser unter Windows, melden sich an und geben den Code ein. Ein Browserfenster kann der Container nicht vor Ihnen öffnen, deshalb der Umweg.

Drei Regeln für Schlüssel und Zugänge, die Sie sich merken sollten:

1. **Nie in `~/.bashrc` eintragen.** Jedes Werkzeug hat einen eigenen Ort für seinen Zugang. Ein Schlüssel in der Startdatei der Shell gilt für alle Programme, auch für solche, die ihn nicht bekommen sollen.
2. **Nie im Befehl tippen.** Alles, was Sie im Terminal eingeben, landet in der Befehlshistorie.
3. **Nie weitergeben.** Die Dateien mit Ihren Zugängen gehören nie in ein Projekt, nie in eine Hilfe-Anfrage, nie in einen Chat. Wer sie hat, arbeitet auf Ihre Rechnung.

## Mitnehmen und pflegen

Drei Dinge gehören zum Alltag.

**Täglich starten.** Nach dem Abmelden oder einem Neustart von Windows läuft der Container nicht mehr. Jeder Arbeitstag beginnt deshalb mit dem Befehl aus Schritt 2 und Enter, das wählt „starten und verbinden“. Ihre Daten sind davon nicht betroffen.

**Aktualisieren.** Die Werkzeuge im Container aktualisieren sich absichtlich nicht selbst, damit alle im Kurs mit derselben, geprüften Fassung arbeiten. Gibt es ein neues Image, wählen Sie im Menü „aktualisieren“. Ihr Home-Verzeichnis bleibt dabei erhalten; was Sie außerhalb davon installiert haben, nicht.

**Mitnehmen.** Sie wissen nicht, ob Sie nächste Woche denselben Rechner antreffen, und vielleicht wollen Sie zu Hause weiterarbeiten. Der Menüpunkt „mitnehmen“ schreibt Ihr komplettes Home-Verzeichnis in eine Datei `home-<datum>.tar` im Ordner `clawbook\sicherungen` Ihres Windows-Profils. Auf einem anderen Rechner wählen Sie im ersten Menü „aus einer Sicherung importieren“, und alles ist wieder da: Projekte, Anmeldungen, Einstellungen. Zwei Hinweise dazu. Die Datei ist oft größer als 4 GB, ein USB-Stick im Format FAT32 kann sie nicht aufnehmen; nehmen Sie exFAT oder NTFS. Und die Datei enthält Ihre Anmeldungen und Ihren privaten Schlüssel. Behandeln Sie sie wie ein Passwort. Auf Poolrechnern, die sich über Nacht zurücksetzen, prüfen Sie am zweiten Tag, ob Ihre Projekte noch da sind, und sichern sonst täglich auf den Stick.

Wenn etwas nicht geht, hat jede Seite der Anleitung dafür einen Abschnitt. Der Weg ist immer derselbe: erst dort nachsehen, dann das Problem erfassen, also Meldung fotografieren oder Text kopieren, und erst dann Hilfe holen. Nennen Sie dabei den Befehl und die vollständige Meldung, aber nie einen Schlüssel oder Anmeldecode. Für den eigenen Mac oder Linux-Rechner beschreibt die Anleitung einen Weg mit Docker oder podman; er ist nicht vom Kurs getestet.

## Die ersten Befehle im Terminal

Sie werden das Terminal nicht viel bedienen, das übernimmt der Agent. Ein paar Befehle brauchen Sie trotzdem, um sich zu bewegen und zu sehen, wo Sie sind. Hier ist das [Cheat-Sheet](../Z-anhang/Z010-glossar.md#cheat-sheet), die kurze Liste zum Nachschlagen:

```bash
pwd              # wo bin ich: zeigt den aktuellen Ordner
ls               # was liegt hier: zeigt die Dateien im Ordner
ls -la           # dasselbe, ausführlich und mit versteckten Dateien
cd lager         # in den Ordner lager wechseln
cd ..            # eine Ebene nach oben
cd ~             # in das Home-Verzeichnis
mkdir lager      # einen Ordner lager anlegen
find . -name "*.md"   # alle Markdown-Dateien ab hier suchen
```

Die Tilde `~` steht für Ihr Home-Verzeichnis, den persönlichen Ordner im Container. Ihre Projekte liegen darunter in `~/source`, geordnet nach Bereichen: `~/source/<Bereich>/<Projekt>`. Ein Beispielprojekt ist schon da, `~/source/samples/primer`; dort können Sie gefahrlos ausprobieren. Der Befehl `wsm` legt neue Projekte in dieser Struktur an und startet Agenten darin, `wsm --help` zeigt seine Möglichkeiten.

Lernen Sie diese Befehle nicht wie Vokabeln. Benutzen Sie sie: Wechseln Sie in das Beispielprojekt, sehen Sie nach, was dort liegt, legen Sie einen Ordner an und gehen Sie wieder zurück. Nach einer Woche sitzen sie.

## Was jetzt klar sein sollte

- Es gibt drei Wege zu einem Agenten: selbst installieren, den gestellten nutzen, clawbook. Die Arbeitsweise ist bei allen dieselbe.
- clawbook ist ein Linux-Rechner als Container in WSL, erreichbar aus PowerShell und VS Code. Die Agenten laufen darin, die Modelle beim Anbieter.
- Einrichten heißt: Voraussetzungen prüfen, ein Befehl, verbinden, VS Code. Danach Zugänge anmelden, ohne Schlüssel in Startdateien, Befehlen oder Chats.
- Projekte und Anmeldungen liegen im Home-Volume. Es lässt sich als eine Datei mitnehmen und ist so wertvoll wie ein Passwort.
- Ein paar Terminalbefehle genügen. Man lernt sie durch Benutzen.

Weiter mit [Die erste Sitzung](A040-die-erste-sitzung.md): ein Ordner, ein Agent, und warum er fragt, ob er diesem Ordner trauen soll.
