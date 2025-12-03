# Création d'un petit jeu de phishing à but éducatif

Simulation de phishing à visée pédagogique. Ce projet permet de sensibiliser les utilisateurs aux risques liés aux faux sites de connexion en leur montrant, de manière ludique et sans danger, comment se protéger et repérer un piège.

## Fonctionnalités
- Formulaire factice : champ email + mot de passe, imitant un portail de connexion.
- Message pédagogique : après soumission, une bannière explique qu’il s’agit d’une simulation et donne des conseils pour repérer un phishing.
- Score local : chaque clic est enregistré anonymement par un identifiant de campagne généré automatiquement (stocké en localStorage).
- Classement collectif : possibilité d’ajouter un lien vers un Google Form pour comparer les scores entre participants.
- Design simple et impactant : couleurs et mise en page inspirées des faux portails pour renforcer l’effet réaliste.

## Vie privée et éthique
- Ce projet est strictement pédagogique. Ne l’utilise pas à des fins malveillantes.
- Aucune donnée d’identification (email/mot de passe) n’est transmise : le formulaire ne stocke ni n’envoie les identifiants saisis. Seule une valeur de compteur anonyme (par identifiant de campagne) est conservée en localStorage pour afficher un score.
- Utilise cette simulation uniquement dans un cadre contrôlé et avec le consentement des personnes testées (formation interne, ateliers, etc.).

## Licence
Projet éducatif et open‑source. Réutilisation libre pour des actions de sensibilisation à la cybersécurité tant que l’utilisation reste pédagogique et non malveillante. (Si tu souhaites une licence formelle, je peux ajouter par exemple MIT, CC BY-NC-SA, etc.)

## Comment l'utiliser
1. Copier le code HTML ci-dessous dans un fichier `index.html`.
2. Ouvrir `index.html` dans un navigateur moderne (ou servir via un serveur statique).
3. Lancer la simulation en cliquant sur "Entrer" : la bannière pédagogique apparaît et le score local est incrémenté.

Important : faites un briefing avant l’exercice et un debrief après pour expliquer les signes de phishing et les bonnes pratiques.


