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

## Code (exemple)
Le code suivant est un exemple autonome que tu peux enregistrer comme `index.html`. Il affiche une fausse page de connexion, affiche une bannière pédagogique après soumission, et gère un petit classement local stocké dans localStorage.

```html
<!doctype html>
<html lang="fr">
<head>
<meta charset="utf-8">
<title>Portail Garelli 95 — Simulation</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="icon" href="garelli-95.png">
<style>
  body { background:#fafafa; font-family:"Courier New", monospace; color:#222; margin:0; }
  .wrap { max-width:600px; margin:40px auto; background:#fff; padding:24px; border-radius:10px; border:2px dashed #444; }
  h2 { margin:0 0 12px; color:#d32f2f; text-align:center; font-family:"Impact", sans-serif; }
  label { display:block; margin:12px 0 6px; font-weight:bold; }
  input[type="email"], input[type="password"] { width:100%; padding:10px; border:1px solid #ccc; border-radius:6px; background:#f9f9f9; }
  .btn { display:inline-block; background:#d32f2f; color:#fff; padding:10px 18px; border:none; border-radius:6px; cursor:pointer; margin-top:14px; font-weight:bold; }
  .btn:hover { background:#f44336; }
  .banner { display:none; margin-top:18px; padding:12px; border-radius:8px; background:#ffe0e0; color:#222; border:1px solid #d32f2f; }
  .tips { margin-top:16px; padding:12px; background:#f5f5f5; border:1px solid #ccc; border-radius:8px; }
  .brand { margin-top:8px; font-size:12px; color:#666; text-align:center; font-style:italic; }
  table { width:100%; border-collapse:collapse; margin-top:16px; }
  th, td { border:1px solid #ccc; padding:8px; text-align:center; }
  th { background:#d32f2f; color:#fff; }
</style>
</head>
<body>
<div class="wrap">
  <h2>Connexion Garelli 95</h2>

  <form id="sensibilisation-form" autocomplete="off" novalidate>
    <label for="mail">Adresse mail</label>
    <input id="mail" type="email" name="mail" placeholder="exemple@domaine.fr" required>
    <label for="pass">Mot de passe</label>
    <input id="pass" type="password" name="password" placeholder="••••••••" required>
    <button class="btn" type="submit">Entrer</button>
  </form>

  <div id="banner" class="banner" role="status" aria-live="polite">
    <strong>⚠ Simulation Garelli 95 — aucune donnée d’identifiable n’a été collectée.</strong>
    <p>Tu viens de tester un faux site de phishing. C’était un exercice pédagogique !</p>
    <div class="tips">
      <ul>
        <li><strong>Regarde l’URL :</strong> un domaine suspect = danger.</li>
        <li><strong>Attention aux urgences :</strong> les pirates cherchent à te presser.</li>
        <li><strong>Indices visuels :</strong> fautes, logos bricolés, incohérences.</li>
        <li><strong>Réflexe :</strong> passe par le portail officiel ou demande à l’IT.</li>
      </ul>
    </div>
    <p><em>Score Garelli 95 :</em> +1 clic enregistré. 🛵</p>
    <p>📊 Consultez le classement collectif sur
      <a href="https://docs.google.com/forms/d/e/1FAIpQLSeom_ddvZ-w7PvbpxGrhkvmegZPZhPfVmzuKp0bi1m1Nnw7Rw/viewform?usp=publish-editor"
         target="_blank" rel="noopener noreferrer">
        Google Form Garelli 95
      </a>
    </p>
  </div>

  <table id="scoreboard" aria-label="Classement local">
    <thead>
      <tr><th>ID campagne</th><th>Clicks</th></tr>
    </thead>
    <tbody></tbody>
  </table>

  <div class="brand">Garelli 95 — Campagne locale ID:
    <span id="cid"></span>
  </div>
</div>

<script>
  // ID de campagne anonyme
  const cidKey = 'garelli_campaign_id';
  const scoresKey = 'garelli_scores';

  const existingCid = localStorage.getItem(cidKey);
  const cid = existingCid || Math.random().toString(36).slice(2, 8);
  localStorage.setItem(cidKey, cid);
  document.getElementById('cid').textContent = cid;

  const form = document.getElementById('sensibilisation-form');
  const banner = document.getElementById('banner');
  const scoreboardBody = document.querySelector('#scoreboard tbody');

  form.addEventListener('submit', function (e) {
    e.preventDefault();

    // On ne conserve pas les identifiants : on réinitialise le formulaire
    form.reset();

    // Affiche la bannière pédagogique
    banner.style.display = 'block';

    // Récupère les scores existants
    let scores = JSON.parse(localStorage.getItem(scoresKey) || '{}');

    // Incrémente le score de cet ID
    scores[cid] = (scores[cid] || 0) + 1;

    // Sauvegarde (local uniquement)
    localStorage.setItem(scoresKey, JSON.stringify(scores));

    // Met à jour le tableau
    updateScoreboard(scores);
  });

  function updateScoreboard(scores) {
    scoreboardBody.innerHTML = '';
    Object.entries(scores).forEach(([id, clicks]) => {
      const row = document.createElement('tr');
      row.innerHTML = `<td>${escapeHtml(id)}</td><td>${Number(clicks)}</td>`;
      scoreboardBody.appendChild(row);
    });
  }

  // Simple échappement pour sécurité d'affichage
  function escapeHtml(str) {
    return String(str)
      .replace(/&/g, '&amp;')
      .replace(/</g, '&lt;')
      .replace(/>/g, '&gt;')
      .replace(/"/g, '&quot;')
      .replace(/'/g, '&#39;');
  }

  // Affiche le tableau au chargement si déjà des scores
  const existingScores = JSON.parse(localStorage.getItem(scoresKey) || '{}');
  if (Object.keys(existingScores).length > 0) {
    banner.style.display = 'block';
    updateScoreboard(existingScores);
  }
</script>
</body>
</html>
```
