# Ludiscore – carnet de parties de jeux de société

Appli web installable (PWA) : elle s'ouvre comme une vraie appli depuis l'écran d'accueil Android, fonctionne sans internet, et garde toutes les données **sur le téléphone**.

Contenu du dossier :

| Fichier | Rôle |
|---|---|
| `index.html` | toute l'appli (interface + logique) |
| `manifest.webmanifest` | nom, icône, couleurs de l'appli installée |
| `sw.js` | permet l'utilisation hors ligne |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | icônes |

---

## 1. Mettre l'appli sur ton téléphone Android (une seule fois, ~5 min)

L'appli doit être servie par une adresse **https** pour pouvoir s'installer. Le plus simple et gratuit : **GitHub Pages**.

1. Sur <https://github.com> (connecté), clique **New repository**.
   - Nom : `ludiscore` · Visibilité : **Public** (obligatoire pour GitHub Pages gratuit ; le dépôt ne contient que le code, **jamais tes données**).
   - Clique **Create repository**.
2. Sur la page du dépôt vide, clique **uploading an existing file**, glisse les **6 fichiers** du dossier (pas le dossier lui-même), puis **Commit changes**.
   *(Ou en ligne de commande : `git init`, `git add .`, `git commit -m "Ludiscore"`, `git remote add origin …`, `git push -u origin main`.)*
3. Dans le dépôt : **Settings → Pages** → *Source* : **Deploy from a branch** → *Branch* : **main** / **(root)** → **Save**.
4. Attends 1 à 2 minutes : l'adresse apparaît en haut de la page Pages, du type
   `https://TON-PSEUDO.github.io/ludiscore/`
5. Sur le téléphone, ouvre cette adresse dans **Chrome** → menu **⋮** → **Installer l'application** (ou **Ajouter à l'écran d'accueil**).
   L'icône Ludiscore apparaît ; elle s'ouvre en plein écran, même sans réseau.

> ⚠️ Les données sont liées à **cette adresse dans ce navigateur**. Utilise toujours la même adresse (l'icône installée), sinon tu verras un carnet vide.

### Mettre à jour l'appli plus tard
Remplace `index.html` dans le dépôt GitHub (*Add file → Upload files*). Au prochain lancement avec internet, le téléphone prend la nouvelle version. **Tes données ne sont pas touchées** (elles sont sur le téléphone, pas sur GitHub).

---

## 2. Sauvegarder ses données (à faire régulièrement)

Tout est enregistré automatiquement sur le téléphone à chaque action. Mais vider les données de Chrome, désinstaller l'appli ou changer de téléphone efface tout. Donc :

- **⚙️ Réglages → Télécharger une sauvegarde** : crée `ludiscore-sauvegarde-AAAA-MM-JJ.json` dans *Téléchargements*.
- **⚙️ Réglages → Envoyer la sauvegarde** : l'envoie directement vers Google Drive, un mail, WhatsApp…
- L'accueil affiche un rappel quand la dernière sauvegarde date de plus de 7 jours.
- **Restaurer** : ⚙️ Réglages → *Restaurer / fusionner une sauvegarde* → choisir le fichier → *Remplacer*.
- **Plusieurs téléphones** : si un ami note des parties sur son propre téléphone, il t'envoie sa sauvegarde et tu choisis *Fusionner* : ses parties s'ajoutent aux tiennes (joueurs et jeux de même nom reconnus, doublons ignorés).
- **Export CSV** : historique complet ouvrable dans Excel / Google Sheets.

### Sauvegarde automatique sur GitHub (recommandé)
Une fois configurée, l'appli envoie toute seule la sauvegarde dans un dépôt GitHub environ 30 secondes après chaque modification (partie, manche de Tarot, joueur…). S'il n'y a pas internet, elle réessaie à la prochaine ouverture. Chaque envoi est un *commit* : GitHub garde l'historique de **toutes les versions**.

1. **Créer le dépôt de sauvegarde** (séparé de celui de l'appli) : github.com → **New repository** → nom `ludiscore-sauvegardes` → public ou privé → coche **Add a README file** → **Create repository**.
2. **Créer un jeton limité à ce dépôt** : photo de profil → **Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens** → **Generate new token** :
   - *Token name* : Ludiscore · *Expiration* : 1 an par exemple ;
   - *Repository access* : **Only select repositories** → `ludiscore-sauvegardes` ;
   - *Permissions* → *Repository permissions* → **Contents : Read and write** (rien d'autre) ;
   - **Generate token**, puis copie le jeton (`github_pat_…`).
3. **Dans l'appli** : ⚙️ Réglages → **Configurer GitHub** → ton pseudo, le nom du dépôt, colle le jeton → **Tester et enregistrer** → *Envoyer*.

Fichiers envoyés dans le dépôt :
- `ludiscore-sauvegarde.json` : joueurs, jeux, parties, manches de Tarot en cours, groupes, réglages d'affichage (thème, minimum de parties) ;
- `historique-parties.csv` : l'historique en tableau, lisible directement sur GitHub.

🔒 **Rien d'autre ne part du téléphone.** Le jeton reste uniquement sur le téléphone : il n'est jamais mis dans les sauvegardes (ni GitHub, ni fichier téléchargé). Les photos de jeux ajoutées sont recompressées par l'appli, sans GPS ni infos de l'appareil. Le jeton ne peut écrire que dans ce dépôt. S'il expire, l'appli l'affiche : crée un nouveau jeton et colle-le dans la configuration.

**Récupérer** (nouveau téléphone, données effacées) : configure GitHub dans l'appli, puis ⚙️ Réglages → **⬇️ Récupérer** → *Remplacer* (ou *Fusionner*).

---

## 3. Guide d'utilisation

Le guide complet est aussi dans l'appli (bouton **?** en haut à droite).

### Démarrer
1. **Jeux** (onglet 🎲) → *Ajouter un jeu* : nom, 1 ou 2 catégories (menu déroulant), façon de gagner.
2. **Joueurs** (onglet 👥) → *Ajouter un joueur* : prénom, couleur, avatar.
3. Bouton **＋ Partie** : jeu → joueurs → points → *Enregistrer*.

Au premier lancement, tu peux choisir *Explorer avec des données d'exemple* pour tester ; elles s'effacent ensuite en un clic sans toucher à tes vraies données.

### Les jeux
- **12 jeux déjà présents** dès le premier lancement, chacun avec une illustration : Les Aventuriers du Rail, Skyjo, Faraway, Courtisans, Château Combo, Moon Colony Bloodbath, Ark Nova, Tarot, Abyss, Catan : Sur la route, Codenames, Citadelles. Pour mettre une vraie photo de ta boîte : fiche du jeu → ✏️ Modifier → 📷 Choisir.
- **18 catégories prévues d'office**, choisies dans un menu (pas de faute de frappe possible) : Stratégie, Familial, Ambiance / Party, Cartes, Jeux de plis, Coopératif, Bluff / Déduction, Enquête / Narratif, Gestion / Engine, Placement d'ouvriers, Deck-building / Draft, Tuiles / Puzzle, Dés / Hasard, Rapidité / Réflexes, Mots / Culture / Quiz, Duel (2 joueurs), Abstrait, Conflit / Négociation. On peut en ajouter dans ⚙️ Réglages si vraiment il en manque.
- **Façon de gagner** : ⬆️ plus de points · ⬇️ moins de points (Skyjo) · 👑 juste le gagnant (sans points) · 👥 en équipes (Coinche, Codenames) · 🤝 coopératif (victoire/défaite collective).
- **Anti-doublon** : un nom déjà pris (même avec accents/majuscules différents) est bloqué ; un nom très proche déclenche un avertissement.
- **Ajout en masse** (onglet Jeux) : une ligne par jeu, `Nom ; Catégorie 1 ; Catégorie 2 ; mode` — l'appli vérifie chaque ligne avant d'ajouter.
- Photo facultative pour chaque jeu.
- Un jeu ou un joueur qui a des parties ne se supprime pas : on l'**archive** (il disparaît des choix, l'historique reste juste).

### Enregistrer une partie
- Jeux récents en premier, recherche en tapant quelques lettres ; création d'un jeu ou d'un joueur possible sans quitter l'écran.
- Raccourcis joueurs : *Comme la dernière partie*, et tes **groupes** (ex. « Coloc »).
- **±** pour les scores négatifs ; égalités gérées (deux premiers = deux victoires).
- **Aperçu du classement** en direct ; le bouton *Enregistrer* reste grisé tant qu'il manque une info (affichée juste au-dessus).
- Alertes : nombre de joueurs inhabituel pour le jeu, date dans le futur, partie identique déjà saisie (doublon).
- La saisie est gardée en **brouillon** si tu quittes l'appli en cours de route.
- Après chaque action : bandeau **Annuler** quelques secondes.
- Corriger : touche la partie dans l'historique → *Modifier*. *Rejouer* relance le même jeu avec les mêmes joueurs.

### 🃏 Feuille de Tarot (parties en plusieurs manches)
- Ouvre la fiche du jeu **Tarot** → **🃏 Feuille de Tarot** (ou choisis Tarot dans **＋ Partie** → « Feuille de Tarot »), puis choisis **3, 4 ou 5 joueurs** (fixes jusqu'à la fin).
- **＋ Nouvelle manche** : preneur, joueur appelé (à 5, ou « seul »), contrat, nombre de bouts, points de l'attaque (bouton ↔️ si tu as compté la défense). Un aperçu montre « réussi / chuté de … » et les points de chacun avant de valider.
- **Annonces & bonus** : petit au bout (attaque ou défense), poignées simple / double / triple, chelem (annoncé réussi, non annoncé réussi, annoncé raté), misère de tête, misère d'atout.
- **Calcul (règle officielle FFT)** : à faire 56 / 51 / 41 / 36 points avec 0 / 1 / 2 / 3 bouts. Chaque défenseur paie (25 + écart ± 10 du petit au bout) × contrat (Petite ×1, Garde ×2, Garde sans ×4, Garde contre ×6), plus la poignée (20 / 30 / 40) au camp gagnant, plus le chelem (+400 / +200 / −200). Le preneur encaisse ce que paient les défenseurs (à 5 avec un appelé : 2 parts pour le preneur, 1 pour l'appelé). Un demi-point d'écart compte comme 1 point. Misère : +10 points pris à chaque adversaire.
- La partie est **enregistrée à chaque manche** : ferme l'appli, reviens jeudi, la partie t'attend (bandeau « Tarot en cours » sur l'accueil). Touche une manche pour la corriger ou la supprimer. Plusieurs parties peuvent être en cours en même temps.
- **🏁 Clôturer la partie** : les totaux deviennent une partie normale (gagnant = plus gros total), comptée dans toutes les statistiques. Dans l'historique, tu peux voir le détail des manches ou **rouvrir** la partie pour la compléter.
- La fiche du Tarot ajoute des stats propres : nombre de prises, % de prises réussies, points moyens par manche.

### Les statistiques (onglet 📊)
Filtres : période, catégorie, jeu.
- **Classement** : % de victoires (minimum de parties réglable), performance, indice vs hasard ; barre colorée selon les catégories des jeux gagnés.
- **Groupe** : choisis A, B, C… → qui finit le plus souvent devant les autres quand ils jouent ensemble, et qui domine sur chaque jeu. Option « exactement ce groupe ».
- **Face-à-face** : A contre B, jeu par jeu ; matrice « qui bat qui » ; meilleurs duos en équipe.
- **Par jeu** : champion de chaque jeu ; la fiche d'un jeu donne son classement, record, score moyen du gagnant, durée moyenne.
- **Par catégorie** : podium par type de jeu.
- **Fiche joueur** : forme récente, séries de victoires, jeu préféré, point fort, bête noire, victime préférée.

Définitions :
- **% de victoires** = parties gagnées / parties jouées (hors coopératif, compté à part).
- **Performance** = part moyenne des adversaires battus (100 % = toujours premier, 0 % = toujours dernier).
- **Indice vs hasard** = victoires / victoires attendues si tout le monde avait le même niveau (×1 = moyenne, ×2 = deux fois mieux).
