# TAAMS Analyzer V3

Analyse les statistiques TikTok sans démonstration fictive.

## Lancer sur ton PC

1. Double-clique sur `demarrer-v3.bat`.
2. Ouvre `http://localhost:3000`.
3. Pour l’analyse rapide, saisis seulement **les vues totales et les likes totaux** d’une période, puis clique sur **Analyser mes totaux**. Les commentaires, partages et abonnés sont facultatifs.
4. Pour comparer chaque vidéo et recevoir des conseils plus précis, ouvre **Je veux ajouter mes vidéos une par une**.

Tu peux aussi importer un CSV ou un JSON. Le modèle CSV vide est disponible sur la page.

## Personnaliser les conseils

Ouvre **Personnaliser les conseils** pour indiquer ton sujet, ton objectif et ta bio. Le bilan du profil et les actions proposées s’appuient sur ces informations et sur les statistiques fournies. Ce sont des conseils automatiques indicatifs, pas des recommandations officielles de TikTok ni une garantie de croissance.

## Publier la version manuelle sur GitHub Pages

GitHub Pages publie le site statique et l’analyse manuelle. Il ne peut pas exécuter le serveur Node requis pour la connexion TikTok.

1. Crée un dépôt GitHub public.
2. Téléverse `index.html`, `app.js`, `style.css` et `exemple-import.csv` à la racine.
3. Dans **Settings → Pages**, choisis **Deploy from a branch**, puis `main` et `/(root)`, et enregistre.
4. Ouvre l’adresse affichée dans la section Pages.

Ne téléverse pas les dossiers `.backup-v1…` ou `.backup-v2…`, ni un fichier `.env` qui contient des clés secrètes.

## Connexion TikTok

La connexion est facultative. Elle nécessite une application TikTok Developer approuvée, Login Kit, Display API, les permissions `user.info.basic`, `user.info.stats` et `video.list`, et un serveur Node accessible en HTTPS. Une page GitHub Pages seule ne suffit pas. La clé secrète doit rester sur le serveur, jamais dans `app.js` ou `index.html`.

- [Guide Login Kit Web](https://developers.tiktok.com/docs/en/login-kit-web)
- [Démarrage Display API](https://developers.tiktok.com/docs/en/display-api-get-started)
- [Autorisations TikTok](https://developers.tiktok.com/docs/en/tiktok-api-scopes)

La connexion officielle récupère les statistiques des vidéos récentes accessibles. La croissance des abonnés sur une période doit être saisie manuellement.

## Confidentialité et limites

Aucun mot de passe TikTok n’est demandé. Les fichiers importés et les chiffres saisis restent dans ton navigateur. Le score TAAMS et les diagnostics sont indicatifs, non officiels.
