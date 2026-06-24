# Quizz CPE — Association CPE

Quiz interactif temps réel (édition Barbecue) : une vue **participant** par défaut et une **console animateur** protégée par mot de passe. Plusieurs téléphones se connectent en direct ; l'animateur pilote la révélation des réponses et le passage à la question suivante.

## Utilisation
- **Participants** : ouvrir le lien, saisir un pseudo, répondre, puis attendre que l'animateur révèle la réponse.
- **Animateur** : ouvrir le lien avec `#animateur` à la fin de l'URL (ou cliquer « Espace animateur »), saisir le mot de passe, ouvrir la salle, partager le QR code, puis « Démarrer le quiz ».

La console animateur affiche : participants actifs, nombre de réponses reçues, votes par option, bouton **Révéler**, bouton **Question suivante**, et le classement en direct.

## Contenu
`quiz-data.json` : 1 question test de participation + 20 QCM (10 sérieux / 10 humour, dont 3 à réponse libre) + 5 charades de difficulté croissante. Une copie est embarquée dans `index.html` comme repli hors-ligne.

## Technique
- Page statique (HTML/CSS/JS, aucune dépendance de build).
- Synchronisation temps réel via **Supabase Realtime** : *Presence* pour compter les participants, *Broadcast* pour l'état du jeu et les réponses (l'animateur fait foi pour le score).
- Configuration en haut du `<script>` dans `index.html` : URL Supabase, clé publique, nom de la salle (`ROOM`) et mot de passe animateur (`ANIMATOR_PASSWORD`).

> Note : le mot de passe animateur est vérifié côté navigateur — il dissuade mais ne protège pas cryptographiquement (le code étant public). Suffisant pour un barbecue ; à ne pas considérer comme un secret.
