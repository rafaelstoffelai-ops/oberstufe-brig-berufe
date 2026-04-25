# Firebase Setup — Fernsteuerung einrichten

Damit du die Präsentation vom Handy steuern kannst (Session-Code, cross-device), braucht es ein **kostenloses Firebase-Konto** (Spark Plan — 0 CHF).

---

## Schritt 1 — Firebase-Projekt erstellen

1. Gehe zu: https://console.firebase.google.com
2. Klicke **"Projekt hinzufügen"**
3. Name: z.B. `oberstufe-brig-2026`
4. Google Analytics: Nein (nicht nötig)
5. Projekt erstellen

---

## Schritt 2 — Realtime Database aktivieren

1. Links im Menü: **"Build" → "Realtime Database"**
2. **"Datenbank erstellen"** klicken
3. Standort: **Europe (belgium)** wählen
4. Startmodus: **Testmodus** (für 30 Tage öffentlich — reicht für die Präsentation)
5. Fertig

---

## Schritt 3 — Web-App registrieren & Config kopieren

1. Zurück zur Projektübersicht (Haus-Icon)
2. **"</> Web"** Icon klicken (App hinzufügen)
3. App-Name: z.B. `praesentation`
4. Firebase Hosting: **Nein** (nicht anhaken)
5. **"App registrieren"** klicken
6. Du siehst jetzt den **firebaseConfig** Block — Beispiel:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "mein-projekt.firebaseapp.com",
  databaseURL: "https://mein-projekt-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "mein-projekt",
  storageBucket: "mein-projekt.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123...:web:abc..."
};
```

---

## Schritt 4 — Config in controller.html eintragen

Öffne `push/controller.html` in einem Texteditor und suche:

```javascript
const FIREBASE_CONFIG = {
  apiKey:            "REPLACE_WITH_YOUR_API_KEY",
  ...
```

Ersetze jeden `REPLACE_WITH_...`-Wert mit deinen echten Werten aus Schritt 3.

---

## Schritt 5 — Testen

1. Öffne `push/index.html` im Browser (oder deployed URL)
2. Öffne `push/controller.html` in einem neuen Tab oder auf dem Handy
3. Wähle **"Presenter"** auf dem Laptop → Code erscheint
4. Wähle **"Controller"** auf dem Handy → Code eingeben → Verbinden
5. Vor/Zurück/Hub-Buttons steuern jetzt die Präsentation!

---

## Troubleshooting

| Problem | Lösung |
|---------|--------|
| "Code nicht gefunden" | Sicherstellen dass Laptop im Presenter-Modus ist und Firebase konfiguriert |
| Controller verbindet nicht | Database-Regeln prüfen (Testmodus muss aktiv sein) |
| Nur gleicher Browser funktioniert | Firebase nicht konfiguriert — FIREBASE_CONFIG Werte prüfen |

---

**Ohne Firebase:** Die Steuerung funktioniert trotzdem — aber nur wenn Laptop und Handy denselben Browser-Tab-Kanal nutzen (gleicher Computer, anderer Tab). Für echte Cross-Device-Kontrolle braucht es Firebase.
