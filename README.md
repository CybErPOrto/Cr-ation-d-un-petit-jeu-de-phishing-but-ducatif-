# Creation-d-un-petit-jeu-de-phishing a but educatif-
Simulation de phishing à but éducatif. Il permet de sensibiliser les utilisateurs aux risques liés aux faux sites de connexion en leur montrant, de manière ludique et sans danger, comment un pirate pourrait tenter de récupérer leurs identifiants. Aucune donnée n’est collectée : tout est stocké localement dans le navigateur via localStorage.

Fonctionnalités
• 	Formulaire factice : champ email + mot de passe, imitant un portail de connexion.
• 	Message pédagogique : après soumission, une bannière explique qu’il s’agit d’une simulation et donne des conseils pour repérer un phishing.
• 	Score local : chaque clic est enregistré anonymement par un identifiant de campagne généré automatiquement.
• 	Classement collectif : possibilité de consulter un Google Form pour comparer les scores entre participants.
• 	Design simple et impactant : couleurs, polices et mise en page inspirées des faux portails pour renforcer l’effet réaliste.


📚 Licence
Projet éducatif et open‑source.
Utilisation libre pour la sensibilisation à la cybersécurité, tant que le but reste pédagogique et non malveillant.


Code :

<!doctype html>

<html lang="fr">
<head>
<meta charset="utf-8">
<title>Portail Garelli 95 — Simulation</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="icon" href="garelli-95.png">
<style>
    body { background:#fafafa; font-family:"Courier New", monospace; color:#222; margin:0; }
    .wrap { max-width:600px; margin:40px auto; background:#fff; padding:24px; border-radius:10px; border:2px dashed #444; }
    h2 { margin:0 0 12px; color:#d32f2f; text-align:center; font-family:"Impact", sans-serif; }
    label { display:block; margin:12px 0 6px; font-weight:bold; }
    input[type="text"], input[type="password"] { width:100%; padding:10px; border:1px solid #ccc; border-radius:6px; background:#f9f9f9; }
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
    <h2>Connexion Garelli 95</h2>
    <form id="sensibilisation-form" autocomplete="off" novalidate>
    <label for="mail">Adresse mail</label>
    <input id="mail" type="text" name="Adresse Mail" placeholder="exemple@domaine.fr" required>
    <label for="pass">Mot de passe</label>
    <input id="pass" type="password" name="Mot de Passe" placeholder="••••••••" required>
    <button class="btn" type="submit">Entrer</button>
    </form>

    <div id="banner" class="banner">
    <strong>⚠ Simulation Garelli 95 — aucune donnée n’a été collectée.</strong>
    <p>Tu viens de tester un faux site de phishing. C’était un exercice pédagogique !</p>
    <div class="tips">
        <ul>
        <li><strong>Regarde l’URL:</strong> domaine suspect = danger.</li>
        <li><strong>Attention aux urgences:</strong> les pirates adorent te presser.</li>
        <li><strong>Indices visuels:</strong> fautes, logos bricolés, incohérences.</li>
        <li><strong>Réflexe:</strong> passe par le portail officiel ou demande à l’IT.</li>
        </ul>
    </div>
    <p><em>Score Garelli 95:</em> +1 clic enregistré. 🛵</p>
     <p>📊 Consultez le classement collectif sur 
        <a href="https://docs.google.com/forms/d/e/1FAIpQLSeom_ddvZ-w7PvbpxGrhkvmegZPZhPfVmzuKp0bi1m1Nnw7Rw/viewform?usp=publish-editor" target="_blank">
          Google Form Garelli 95
        </a>
      </p>
    </div>

    <div class="brand">Garelli 95 — Campagne locale ID:
    <span id="cid"></span>
    </div>
</div>

<script>
    // ID de campagne anonyme
    const cid = localStorage.getItem('garelli_campaign_id') || Math.random().toString(36).slice(2, 8);
    localStorage.setItem('garelli_campaign_id', cid);
    document.getElementById('cid').textContent = cid;

    const form = document.getElementById('sensibilisation-form');
    const banner = document.getElementById('banner');
    const scoreboard = document.querySelector('#scoreboard tbody');

    form.addEventListener('submit', function (e) {
      e.preventDefault();
      form.reset();
      banner.style.display = 'block';

      // Récupère les scores existants
      let scores = JSON.parse(localStorage.getItem('garelli_scores') || '{}');

      // Incrémente le score de cet ID
      scores[cid] = (scores[cid] || 0) + 1;

      // Sauvegarde
      localStorage.setItem('garelli_scores', JSON.stringify(scores));

      // Met à jour le tableau
      updateScoreboard(scores);
    });

    function updateScoreboard(scores) {
      scoreboard.innerHTML = '';
      Object.entries(scores).forEach(([id, clicks]) => {
        const row = document.createElement('tr');
        row.innerHTML = `<td>${id}</td><td>${clicks}</td>`;
        scoreboard.appendChild(row);
      });
    }

    // Affiche le tableau au chargement si déjà des scores
    const existingScores = JSON.parse(localStorage.getItem('garelli_scores') || '{}');
    if (Object.keys(existingScores).length > 0) {
      banner.style.display = 'block';
      updateScoreboard(existingScores);
    }
  </script>
</body>
</html>
