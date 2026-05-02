# 🔥 Lab 18 – FireStorm

**Difficulté :** Medium  
**Techniques :** Reverse Android (Jadx), Hooking Frida, Firebase Auth

---

## 🎯 Objectif

L'APK contient une méthode `Password()` jamais appelée. Il faut la forcer via Frida pour s'authentifier à Firebase et lire le flag.

---

## 🔍 Étape 1 – Analyse statique (Jadx)

- APK décompilé dans **Jadx-GUI**
- `MainActivity.Password()` construit un mot de passe avec 6 strings partielles + `generateRandomString()` native
- Email Firebase hardcodé : `TK757567@pwnsec.xyz`

---

## 💉 Étape 2 – Extraction Frida

**Script `extract_now.js` :**
```javascript
Java.perform(function() {
    Java.choose('com.pwnsec.firestorm.MainActivity', {
        onMatch: function(instance) {
            console.log("[+] " + instance.Password());
        },
        onComplete: function() {}
    });
});
```

**Commande :** `frida -U -l extract_now.js Firestorm`  
**Mot de passe :** `C7_dotpsC7t7f_._In_i.IdttpaofoaIIdIdnndIfC`

![Frida extraction result](https://github.com/user-attachments/assets/3ef58286-e413-491c-a29e-3cce415d0e1c)

---

## 🔐 Étape 3 – Authentification Firebase

![Firebase authentication](https://github.com/user-attachments/assets/4d7ad405-dc61-48a7-898f-39b025724cee)

---

## 🚩 Flag

![Flag result](https://github.com/user-attachments/assets/f6896f18-ccb7-4697-b49f-51ed82cc9115)