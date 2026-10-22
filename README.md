# Voyage entre amis

Site d'organisation d'un voyage (programme, vols, logement, activités). Un seul `index.html`, sans framework ni étape de build, publié avec GitHub Pages.

## Comment ça marche

- Les données sont dans `trip.json`, sur la branche `data` (créée automatiquement à la première modification). Cette branche ne relance pas la publication du site.
- **Tout est chiffré** dans le navigateur (AES-GCM 256, clé dérivée du code par PBKDF2-SHA-256, 210 000 itérations, sel aléatoire) avant d'être envoyé. Le dépôt est public, mais `trip.json` n'est qu'un texte illisible sans le code. Les messages de commit sont génériques.
- Pour modifier, il faut une **clé d'édition** : un token GitHub fine-grained limité à ce dépôt (Contents : Read and write). Elle est transmise par un lien `…/#cle=TOKEN`, enregistrée dans le navigateur puis retirée de l'adresse. Le **code** n'est jamais dans le lien : il est saisi sur la page d'accueil.
- Sans clé, le site est en lecture seule (après saisie du code).
- Chaque modification est un commit. Si le fichier a changé entre-temps (409/422), le site recharge la dernière version et rejoue la modification dessus (6 essais maximum). Rien n'est écrasé.
- Hors ligne : dernière version en cache, modifications mises en attente puis envoyées au retour du réseau.
- Hors `github.io` : mode local, données dans le navigateur. Pour un domaine personnalisé, ajouter avant le script principal : `<script>window.TRIP_CONFIG = { owner: "compte", repo: "depot" };</script>`.

Le champ « Infos privées » de chaque fiche est stocké dans le fichier chiffré : il est protégé par le même code.

## Mise en route

1. Créer la clé d'édition sur <https://github.com/settings/personal-access-tokens/new> (dépôt unique, Contents : Read and write, expiration après le voyage). Ne jamais l'écrire dans un fichier du dépôt.
2. Ouvrir le site avec `…/#cle=TOKEN`, choisir le code du voyage, ajouter les photos.
3. Réglages → Copier le lien d'édition → l'envoyer aux voyageurs, puis leur donner le code à part.

## Fichiers

`index.html` · `manifest.webmanifest` · `sw.js` · `icon-192.png` · `icon-512.png` · `apple-touch-icon.png` · `.nojekyll`
