# **Cahier des charges — Application mobile Coran (FR \+ Tafsir en Wolof)**

## **1\. Présentation du projet**

L’application mobile a pour objectif de rendre le **Coran accessible en français**, avec la possibilité d’écouter le **tafsir (explication)** en **wolof** réalisé par des **hafiz sénégalais**. L’expérience utilisateur doit favoriser la compréhension, l’apprentissage et la spiritualité, tout en valorisant la culture islamique sénégalaise.

Stack technologique : **Laravel (Backend/API)** \+ **Expo/React Native (Frontend mobile)**.

---

## **2\. Objectifs principaux**

* Offrir une **lecture fluide du Coran** avec texte arabe, traduction française et translittération.

* Permettre l’écoute et le téléchargement du **tafsir en wolof** par sourate ou verset.

* Proposer une interface intuitive et adaptée à la lecture quotidienne.

* Permettre la **recherche par mots-clés** (arabe ou français).

* Intégrer un mode hors ligne pour la consultation sans connexion.

---

## **3\. Fonctionnalités principales**

### **a. Accueil**

* Présentation des sourates et versets.

* Accès rapide à la dernière lecture.

### **b. Lecture du Coran**

* Texte arabe avec vocalisation.

* Traduction française officielle (API AlQuran Cloud – version *“quran-uthmani”* et *“fr.hamidullah”*).

* Translittération française pour faciliter la prononciation.

* Navigation par sourate, verset, ou thème.

### **c. Tafsir (exégèse en wolof)**

* Audio par hafiz sénégalais, organisés par sourate.

* Possibilité de téléchargement ou d’écoute en streaming.

* Synchronisation entre texte et audio.

### **d. Recherche**

* Recherche multilingue (arabe, français, translittération).

* Filtres par sourate, verset ou mot-clé.

### **e. Profil utilisateur**

* Historique des lectures et audios écoutés.

* Marque-pages et favoris.

* Mode nuit et personnalisation de la taille du texte.

### **f. Mode hors ligne**

* Mise en cache locale des traductions et audios téléchargés.

---

## **4\. Architecture technique**

### **Backend (Laravel)**

* **Framework :** Laravel 11\.

* **API RESTful** exposant les endpoints pour :

  * Lecture et recherche du texte du Coran.

  * Consultation et téléchargement des tafsirs.

  * Gestion des utilisateurs et des favoris.

* **Intégration de l’API AlQuran Cloud** :

  * Endpoint : `https://api.alquran.cloud/v1/`.

  * Endpoints utilisés :

    * `/quran/fr.hamidullah` pour la traduction française.

    * `/quran/uthmani` pour le texte arabe.

    * `/ayah/{ayahNumber}/ar.fr.hamidullah` pour une recherche par verset.

  * Les données seront **mises en cache** dans Redis pour optimiser les performances et réduire les appels externes.

  * Synchronisation planifiée (via cron Laravel) pour mettre à jour les données hebdomadairement.

* **Fallback hors ligne** : si l’API est inaccessible, les données seront servies depuis la base locale (PostgreSQL ou MySQL).

### **Gestion du tafsir**

* Les fichiers audio des hafiz seront hébergés sur **AWS S3** ou un équivalent (DigitalOcean Spaces).

* Une table `tafsirs` reliera chaque fichier audio à la sourate correspondante.

### **Sécurité et Authentification**

* Authentification via **Laravel Sanctum**.

* Chiffrement des données sensibles.

* Stockage sécurisé des préférences utilisateur.

---

## **5\. Frontend mobile (Expo / React Native)**

* **Stack :** Expo SDK 52+, React Navigation, Zustand ou Redux pour l’état global.

* **Intégration API Laravel** pour récupérer les données de sourates, traductions et audios.

* **Lecture audio** via Expo AV.

* **UI** moderne, minimaliste et inspirée des applications islamiques (vert émeraude, doré, blanc cassé).

* **Mode hors ligne** : AsyncStorage pour conserver les données téléchargées.

---

## 

## **6\. Hébergement & Déploiement**

* **Backend** : hébergement sur VPS (Ubuntu 22.04, Nginx, PHP 8.3).

* **Base de données** : PostgreSQL.

* **Stockage des audios** : AWS S3 / DigitalOcean Spaces.

* **App mobile** : publication sur Google Play & App Store via **Expo EAS Build**.

---

## **7\. Roadmap de développement**

1. **Phase 1 — Prototype (MVP)**

   * Intégration API AlQuran Cloud.

   * Lecture du Coran (texte arabe \+ traduction française).

   * Tafsir audio par sourate (intégration d’un hafiz pilote).

2. **Phase 2 — Version complète**

   * Translittération française.

   * Ajout de plusieurs hafiz et tafsirs.

   * Recherche avancée et favoris.

   * Mode hors ligne complet.

3. **Phase 3 — Optimisation**

   * Amélioration de la recherche.

   * Statistiques d’écoute et recommandations.

   * Internationalisation (anglais, arabe).

---

## **8\. Maintenance & Scalabilité**

* Monitoring via Laravel Telescope et Sentry.

* Backups automatiques (DB \+ fichiers audio).

* Tests automatisés (PestPHP \+ Jest).

* Architecture scalable avec séparation Backend / CDN / API publique.

---

## **9\. Annexes**

* Documentation de l’API : [https://alquran.cloud/api](https://alquran.cloud/api)

* Exemple de requête : `GET https://api.alquran.cloud/v1/quran/fr.hamidullah`

* Exemple de réponse : contient le texte arabe, traduction française et identifiants de versets.

---

**Responsable technique :** à définir  
 **Technologies principales :** Laravel 11, Expo React Native 52, PostgreSQL, AWS S3  
 **Langues :** Arabe, Français, Wolof (audio tafsir).

