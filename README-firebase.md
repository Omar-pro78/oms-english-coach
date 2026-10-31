# OMS English Coach — passage en site autonome (GitHub Pages + Firebase)

Ce dossier contient la version "hors Claude" de l'app : `index.html` + le dossier `audio/`
(311 fichiers mp3). Hébergée sur GitHub Pages, elle n'est plus dans l'iframe sandboxée de
Claude — c'est ce qui bloquait le micro. Avec Firebase en plus, ta progression (phrases
maîtrisées, série de jours, session du jour) se synchronise entre tous tes appareils.

Ce fichier explique uniquement la partie que SEUL toi peux faire (créer tes comptes/projets).
Le reste (créer le dépôt GitHub, y mettre les fichiers, activer GitHub Pages), je peux le
faire pour toi si tu me donnes 30 secondes pour une connexion `gh` — voir le message associé.

## Étape 1 — Créer le projet Firebase (5 min)

1. Va sur https://console.firebase.google.com (connecte-toi avec ton compte Google).
2. Clique **"Ajouter un projet"**, donne-lui un nom (ex. `oms-english-coach`), continue avec
   les options par défaut (pas besoin de Google Analytics), puis **"Créer le projet"**.

## Étape 2 — Activer la connexion Google (Authentication)

1. Dans le menu de gauche : **Build > Authentication**.
2. Onglet **"Sign-in method"** (méthode de connexion).
3. Clique sur **"Google"** dans la liste des fournisseurs, active-le (toggle), choisis un
   email de support (le tien), **Enregistrer**.

## Étape 3 — Activer Firestore (la base qui stocke ta progression)

1. Menu de gauche : **Build > Firestore Database**.
2. **"Créer une base de données"**.
3. Choisis une région proche (ex. `eur3 (europe-west)`), mode **production**.
4. Une fois créée, onglet **"Règles"** (Rules) : remplace tout le contenu par celui du
   fichier `firestore.rules` fourni dans ce dossier, puis **Publier**.

## Étape 4 — Récupérer la config et me l'envoyer

1. Menu de gauche, en haut : icône ⚙️ **"Paramètres du projet"**.
2. Onglet **Général**, descends jusqu'à **"Vos applications"**.
3. Clique sur l'icône **`</>`** (Web) pour ajouter une appli web. Donne-lui un nom
   (ex. `oms-coach-web`), PAS besoin de cocher "Firebase Hosting". **Enregistrer l'application**.
4. Firebase affiche un bloc `const firebaseConfig = { apiKey: "...", ... }`.
   **Copie-colle ces 6 valeurs** (apiKey, authDomain, projectId, storageBucket,
   messagingSenderId, appId) et envoie-les-moi dans le chat — je les insère dans
   `index.html` à ta place (elles ne sont pas secrètes : ce sont des identifiants publics
   côté client, la vraie sécurité vient des règles Firestore de l'étape 3).

## Étape 5 — Autoriser le domaine GitHub Pages

Une fois le site en ligne (après l'étape GitHub), Firebase doit savoir qu'il a le droit
de s'y connecter :

1. **Authentication > Settings > Authorized domains** (Domaines autorisés).
2. **Ajouter un domaine**, entre ton domaine GitHub Pages (ex. `tonpseudo.github.io`).
3. Enregistre.

Sans cette étape, le bouton "Se connecter" affichera une erreur `auth/unauthorized-domain`.

## Et le micro, ça marchera vraiment ?

Oui, dans Chrome (et la plupart des navigateurs modernes) sur un vrai site HTTPS comme
GitHub Pages — plus besoin de l'autorisation qui échouait dans l'iframe de Claude. Chrome
te demandera l'autorisation micro une seule fois, normalement.
