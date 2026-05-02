# LAB1-SECURITE
# Mobexler — Environnement de Pentest Mobile

## Qu'est-ce que Mobexler ?

Mobexler est une **machine virtuelle (VM) spécialisée** dans le pentest d'applications mobiles Android et iOS. Basée sur une distribution Linux légère, elle regroupe dans un seul environnement tous les outils nécessaires à l'audit de sécurité mobile, sans installation manuelle fastidieuse.

Elle tourne sous **VirtualBox** (ou VMware) et s'utilise directement depuis n'importe quel PC hôte Windows, macOS ou Linux.

---

## Pourquoi utiliser Mobexler ?

### Le problème sans Mobexler
Monter un environnement de pentest mobile from scratch est long et complexe :
- Installer ADB, Frida, Burp Suite, apktool, jadx...
- Gérer les conflits de versions
- Configurer les certificats proxy sur l'émulateur
- Rooter ou patcher les APKs manuellement

### Ce que Mobexler résout
Tous ces outils sont **pré-installés, pré-configurés et prêts à l'emploi**. On lance la VM et on commence à tester immédiatement.

---

## Ce que contient Mobexler

| Catégorie | Outils inclus |
|---|---|
| Analyse statique | jadx, apktool, dex2jar, androguard |
| Analyse dynamique | Frida, objection, Xposed |
| Proxy / Trafic réseau | Burp Suite, mitmproxy, Wireshark |
| ADB & émulation | adb, Android SDK tools |
| Reverse engineering | Ghidra, strings, binwalk |
| Exploitation | Metasploit, drozer |
| Divers | Python3, Node.js, Git, VS Code |

---

## Architecture typique d'utilisation

```
┌─────────────────────────────────┐
│        PC Hôte (Windows)        │
│                                 │
│  ┌──────────────────────────┐   │
│  │   Android Studio AVD     │   │
│  │   (émulateur Android)    │   │
│  └────────────┬─────────────┘   │
│               │ ADB (TCP)       │
│  ┌────────────▼─────────────┐   │
│  │     VM Mobexler          │   │
│  │  (outils de pentest)     │   │
│  │  IP : 10.0.2.15          │   │
│  │  Gateway hôte : 10.0.2.2 │   │
│  └──────────────────────────┘   │
└─────────────────────────────────┘
```

Mobexler se connecte à l'émulateur via ADB over TCP pour analyser, intercepter et manipuler l'application cible.

---

## Cas d'usage concrets

- **Analyser DIVA** (Damn Insecure and Vulnerable App) pour apprendre les vulnérabilités Android courantes
- **Intercepter le trafic HTTPS** d'une application avec Burp Suite + certificat installé sur l'émulateur
- **Hooker des fonctions** à la volée avec Frida pour bypasser la détection de root ou le SSL pinning
- **Décompiler un APK** avec jadx pour lire le code source Java/Kotlin obfusqué
- **Tester les stockages insécurisés** (SharedPreferences, SQLite, fichiers en clair)

---

## Connexion ADB depuis Mobexler vers l'émulateur Android Studio

L'émulateur tournant sur l'hôte Windows, on utilise l'IP de la gateway VirtualBox :

```bash
# Depuis le terminal Mobexler
adb connect 10.0.2.2:5555
adb devices
```

Sur l'hôte Windows (cmd) :
```cmd
adb forward tcp:5555 tcp:5554
```

---

## Screenshot depuis la realisation de ce lab
<img width="263" height="103" alt="devices" src="https://github.com/user-attachments/assets/68c71bb7-876e-4280-a7e8-cda76dc86a7a" />
<img width="959" height="496" alt="demarrage" src="https://github.com/user-attachments/assets/f7ffc6c7-a5a9-49ab-b2e3-8a3b99b17b4a" />
<img width="960" height="494" alt="acceuil" src="https://github.com/user-attachments/assets/eb8d31b0-d824-4f5a-ba18-33cbcd4f639b" />
<img width="960" height="494" alt="snapshot" src="https://github.com/user-attachments/assets/e0276647-b8a8-4512-9cd1-9fda17e838e0" />
<img width="722" height="375" alt="ip" src="https://github.com/user-attachments/assets/056355f8-dfb4-4cfd-b63a-c50014301100" />
<img width="524" height="71" alt="installation de mobexler" src="https://github.com/user-attachments/assets/3a5cf8bf-df67-46dd-aee9-56b759e9d843" />
<img width="960" height="494" alt="import-mobexler" src="https://github.com/user-attachments/assets/a16a8af1-2108-48c6-9704-01a503adb74a" />
<img width="542" height="76" alt="hash" src="https://github.com/user-attachments/assets/de4276aa-f65e-45ba-b7c4-2e588ebcd5f0" />
