# QuizShow Live – kostenlose Online-Quizshow

Diese Website ist ein einfacher Multiplayer-Jeopardy-Prototyp: Eine Person erstellt das Spiel und teilt den fünfstelligen Code. Alle Spieler öffnen dieselbe Website und treten mit ihrem Handy bei. Die Spielleitung öffnet Fragen und verwaltet Punkte; Frage, Antwort, Bild, YouTube-Einbettung und Punktestand werden an die verbundenen Geräte gesendet.

## 1. Kostenlose Online-Verbindung einrichten (Supabase)

1. Öffne https://supabase.com/ und erstelle ein kostenloses Konto.
2. Erstelle ein neues Projekt. Bewahre das Datenbankpasswort sicher auf.
3. Öffne im Projekt **Project Settings → API** (bei der neuen Oberfläche: **Connect** oder **API Keys**).
4. Kopiere die **Project URL** und den **anon/public key** bzw. **publishable key**.
5. In QuizShow Live trägst du diese beiden Werte ein und klickst auf **Online verbinden**.

Die Website nutzt Supabase Realtime Broadcast-Channels. Es ist keine Datenbanktabelle und kein SQL-Skript nötig. Das Spiel wird während der Sitzung über einen öffentlichen Broadcast-Kanal geteilt. **Wichtig:** Öffentliche Kanäle sind nicht vertraulich: Wer den Spielcode kennt und die Projekt-URL/den öffentlichen Schlüssel hat, könnte versuchen, den Kanal zu abonnieren oder Nachrichten zu senden. Verwende keine privaten Daten und teile nur den Spielcode mit den gewünschten Mitspielern. Ein öffentlicher anon/publishable key ist für Browser-Apps vorgesehen; niemals einen `service_role`- oder Secret-Key in diese Website eintragen.

## 2. Kostenlos veröffentlichen (GitHub Pages)

1. Erstelle oder melde dich bei https://github.com/ an.
2. Erstelle ein neues Repository, zum Beispiel `quizshow-live`. Für eine einfache kostenlose Veröffentlichung kann es **Public** sein.
3. Lade die Datei `index.html` aus diesem Paket in das Repository hoch (Add file → Upload files → Commit changes).
4. Gehe im Repository zu **Settings → Pages**.
5. Unter **Build and deployment** wähle **Deploy from a branch**.
6. Wähle den Branch `main` und den Ordner `/(root)`, dann **Save**.
7. Warte ein bis drei Minuten. GitHub zeigt danach die Website-Adresse im Pages-Bereich an.
8. Öffne die Adresse, gib Supabase Project URL und den öffentlichen anon/publishable key ein, und verbinde dich. Teile den Link deiner Website und den Spielcode mit deinen Freunden.

GitHub Pages ist statisches Hosting; die Live-Kommunikation kommt von Supabase Realtime.

## 3. So spielt ihr

- Die Spielleitung öffnet die Website, verbindet Supabase und klickt **Spiel erstellen**.
- Teile den fünfstelligen Spielcode und den Website-Link.
- Freunde öffnen den Link, geben ihren Namen und den Spielcode ein und tippen **Beitreten**.
- Die Spielleitung tippt ein Punktefeld, bearbeitet die Frage und kann Antwort und Punkte anzeigen/vergeben.
- Zum Hinzufügen von Videos nutze normale YouTube-Links wie `https://www.youtube.com/watch?v=VIDEO_ID`. Manche Videos erlauben kein Einbetten, und YouTube kann Werbung anzeigen.
- Für Bilder funktioniert ein direkter öffentlicher Bildlink oder ein kleines Bild, das von deinem Gerät hochgeladen wird.

## Einschränkungen dieses Prototyps

- Die Website ist ein Startprototyp, kein gehärteter Produktionsdienst. Der Spielcode ist kurz und nicht als Sicherheitsmechanismus gedacht.
- Ein Spiel wird nicht auf einem Server dauerhaft gespeichert. Wenn die Spielleitung die Seite neu lädt, kann sie den gespeicherten Entwurf aus ihrem Browser wiederherstellen, aber eine bestehende Online-Sitzung kann getrennt werden. Für zuverlässiges Wiederbeitreten braucht es Datenbank-Persistenz.
- Der Spielcode ist nicht exklusiv reserviert. Wenn zwei Hosts zufällig denselben Code erhalten, sollten sie ein neues Spiel starten.
- Team-Punkte werden durch die Spielleitung vergeben. Spielergeräte zeigen die geteilten Fragen und den Punktestand.
- Bilder werden als Daten im Browserzustand übertragen; sehr große Bilder können Broadcast-Limits erreichen. Kleine Bilder (unter ca. 1,5 MB) verwenden.
- YouTube-Shorts, altersbeschränkte Videos, private Videos oder Videos mit deaktivierter Einbettung funktionieren möglicherweise nicht direkt eingebettet.
- Dieses Beispiel sendet Spielinhalte an alle Geräte im selben Raum; verwende es nicht für private oder vertrauliche Inhalte.

## Dateien

- `index.html` – die Quiz-Website
