# 📱 SecureChat – Vollständige Anleitung
## APK bauen & Firebase einrichten (NUR mit Handy!)

---

## 🔥 SCHRITT 1: Firebase einrichten (kostenlos, 5 Minuten)

1. Gehe auf **console.firebase.google.com** in deinem Handy-Browser
2. Klicke auf **"Projekt erstellen"**
3. Name: `SecureChat` → Weiter → Weiter → Erstellen
4. Klicke auf das **Android-Symbol** (</> oder Android-Logo)
5. **Paketname eingeben:** `com.securechat.app`
6. App registrieren → Weiter
7. **`google-services.json` herunterladen** → speichere sie gut!
8. Weiter → Weiter → Fertig

**Realtime Database aktivieren:**
1. Links im Menü: **"Realtime Database"** → Datenbank erstellen
2. Wähle **"Im Testmodus starten"** (für Entwicklung)
3. Fertig!

---

## 🏗️ SCHRITT 2: APK online bauen (kostenlos, kein PC!)

### Option A: GitHub Actions (empfohlen)

1. **GitHub-Account erstellen** (falls noch nicht vorhanden): github.com
2. Neues Repository erstellen: **"SecureChat"** → Public → Create
3. Alle Code-Dateien hochladen (aus dem ZIP)
4. Die `google-services.json` in den Ordner `app/` hochladen
5. Gehe zu **Actions** → **"New workflow"** → **"set up a workflow yourself"**
6. Füge folgenden Code ein:

```yaml
name: Build APK
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: Build APK
        run: ./gradlew assembleDebug
      - uses: actions/upload-artifact@v3
        with:
          name: SecureChat-APK
          path: app/build/outputs/apk/debug/app-debug.apk
```

7. Klicke **"Commit changes"**
8. Gehe zu **Actions** → warte ~5 Minuten
9. Klicke auf den fertigen Build → **"Artifacts"** → **SecureChat-APK herunterladen** 🎉

### Option B: Buildozer Online / AppCircle
- Registriere dich auf **appcircle.io** (kostenlos)
- Verbinde dein GitHub-Repository
- Build starten → APK herunterladen

---

## 📲 SCHRITT 3: APK auf dem Handy installieren

1. Einstellungen → **"Unbekannte Quellen"** oder **"Apps aus unbekannten Quellen"** aktivieren
   - Bei neueren Android: Einstellungen → Sicherheit → Apps installieren → Browser/Dateien → Erlauben
2. Die heruntergeladene `app-debug.apk` öffnen
3. **Installieren** klicken
4. App öffnen → Du bekommst automatisch deine lange zufällige ID!

---

## 💬 So funktioniert die App

1. **Beim ersten Start:** App generiert automatisch eine einzigartige 32-stellige ID für dich
2. **Deine ID teilen:** Klicke auf "Kopieren" und schicke die ID deinem Freund (per WhatsApp, SMS, etc.)
3. **Kontakt hinzufügen:** Klicke "+ Kontakt hinzufügen" → ID des Freundes eingeben
4. **Chatten:** Auf den Chat klicken → Nachrichten schreiben!

---

## ⚠️ Wichtige Hinweise

- Die App nutzt **Firebase Realtime Database** als Server (kostenlos bis 1 GB Speicher & 10 GB Traffic/Monat)
- **Keine E-Mail, kein Passwort** – nur die ID zählt
- Wer deine ID kennt, kann dir schreiben → Teile sie nur mit Leuten denen du vertraust
- Die kostenlose Firebase-Version reicht für persönliche Nutzung völlig aus

---

## 📁 Dateistruktur für GitHub

```
SecureChat/
├── app/
│   ├── src/main/
│   │   ├── java/com/securechat/app/
│   │   │   ├── MainActivity.kt
│   │   │   ├── ChatActivity.kt
│   │   │   ├── Models.kt
│   │   │   └── Adapters.kt
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   │   ├── activity_main.xml
│   │   │   │   ├── activity_chat.xml
│   │   │   │   ├── item_message.xml
│   │   │   │   └── item_chat.xml
│   │   │   ├── drawable/
│   │   │   │   ├── bg_message_sent.xml
│   │   │   │   └── bg_message_received.xml
│   │   │   └── values/
│   │   │       └── strings.xml
│   │   └── AndroidManifest.xml
│   ├── google-services.json  ← VON FIREBASE HERUNTERLADEN!
│   └── build.gradle
├── build.gradle
└── settings.gradle
```

---

## ❓ Probleme?

**"google-services.json nicht gefunden"** → Stelle sicher, dass die Datei im `app/` Ordner liegt

**"Build fehlgeschlagen"** → Prüfe ob alle Dateien hochgeladen sind

**"Nutzer nicht gefunden"** → Beide Personen müssen die App mindestens einmal geöffnet haben, damit ihre ID registriert wird

---

*SecureChat – Einfach. Anonym. Sicher.*
