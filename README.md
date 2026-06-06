
# Lab 14 - Bypass Root Detection Android

## Objectif
Contourner la détection de root sur Android avec Frida et Objection.

## Installation rapide

```bash
# Installer Frida
pip install frida-tools

# Installer Objection
pip install objection
```

## Commandes principales

### 1. Lancer frida-server sur l'appareil
```bash
adb push frida-server /data/local/tmp/
adb shell chmod 755 /data/local/tmp/frida-server
adb shell /data/local/tmp/frida-server &
```

### 2. Bypass avec Frida
```bash
frida -U -f nom.app.package -l bypass.js
```

### 3. Bypass avec Objection
```bash
objection -g nom.app.package explore
android root disable
```

## Script Frida minimal (bypass.js)

```javascript
Java.perform(function() {
    // Forcer le statut non-root
    var Build = Java.use('android.os.Build');
    Build.TAGS.value = 'release-keys';
    console.log('[✔] Root bypass activé');
});
```

## Vérifications

```bash
# Tester la connexion
frida-ps -U

# Voir les logs
frida -U -f nom.app.package -l bypass.js --no-pause
```
