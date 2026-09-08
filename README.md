# 🗣️ EiM Vocabulary & Pronunciation App

Une application web de type Flashcards simple et légère, sans publicité ni connexion, conçue pour un apprentissage du vocabulaire axé sur la prononciation.

---

## 🌟 Fonctionnalités principales

* **🎴 Flashcards 3D & Mode Liste** : Basculez entre une vue de cartes mémoire à retourner (effet 3D) et une vue liste compacte.
* **🔊 Synthèse vocale (Web Speech API)** : Écoutez la prononciation native des mots en anglais (avec choix de l'accent : 🇬🇧 UK, 🇺🇸 US, 🇦🇺 AU) et en français.
* **🎛️ Contrôle de la vitesse** : Ajustez la vitesse d'élocution (de 0.5x à 1.2x) via un curseur dédié.
* **🔤 Phonétique (API)** : Affichage optionnel de la transcription phonétique internationale.
* **⭐ Cartes favorites** : Marquez les mots pour vous constituer une liste d'entraînement personnalisée.
* **🟢🟡🔴 Évaluation de la difficulté** : Auto-évaluez chaque mot pour suivre votre progression et trier vos cartes du plus difficile au plus facile.
* **🔍 Recherche & Tri en temps réel** : Filtrez par mot-clé, triez par ordre alphabétique, par niveau de difficulté ou mélangez aléatoirement.
* **🎮 Jeu d'écoute ("Listen & Point")** : Entraînez votre compréhension orale de manière ludique grâce au jeu associé.
* **🚫 Anti-Traduction automatique** : Balises intégrées pour empêcher les navigateurs de traduire automatiquement la page et de fausser l'exercice.

---

## 💾 Sauvegarde des données (Local Storage)

Les sélections de difficultés et les étoiles sont conservées directement dans le navigateur de l'utilisateur grâce à l'API **`localStorage`** du Web HTML5. Aucun compte ni serveur distant n'est requis.

### 1. Clés de stockage dédiées
Au début du script, deux clés distinctes sont définies pour structurer les données :
* `RATINGS_STORAGE_KEY` (sauvegardée sous `'vocab_app_ratings_v1'`) pour les évaluations de difficulté (🟢, 🟡, 🔴).
* `STARRED_STORAGE_KEY` (sauvegardée sous `'vocab_app_starred_v1'`) pour les cartes favorites (étoiles).

### 2. Lecture et écriture (JSON)
Les données sont manipulées sous forme d'objets JavaScript, puis converties en texte au format JSON pour être acceptées par le navigateur :
* **Chargement (`getStoredRatings` / `getStoredStarred`)** : À l'ouverture de la page, le code récupère la chaîne textuelle enregistrée et la transforme à nouveau en objet avec `JSON.parse()`.
* **Sauvegarde (`saveStoredRating` / `saveStoredStarred`)** : À chaque fois que l'utilisateur clique sur une étoile ou modifie la difficulté d'un mot, l'état correspondant est mis à jour dans l'objet, puis sauvegardé instantanément avec `localStorage.setItem(KEY, JSON.stringify(data))`.

### 3. Identification unique des cartes (`cardId`)
Pour éviter toute confusion entre les cartes d'unités différentes, chaque mot reçoit un identifiant unique combinant l'unité et son ID (ex: `eim9_u1_3`). C'est cet identifiant complet qui sert de clé dans les objets enregistrés, garantissant que vos évaluations et étoiles restent bien attribuées au bon mot dans la bonne unité.

### Caractéristiques clés de ce stockage
* **Persistance permanente** : Les données ne s'effacent pas à la fermeture de l'onglet ou du navigateur. Elles restent conservées d'une session à l'autre.
* **100% Local & Privé** : Aucune donnée n'est envoyée vers un serveur distant ; tout reste sur la machine/l'appareil de l'utilisateur.
* **Limitation** : Si l'utilisateur change d'appareil, de navigateur ou vide l'historique/cache complet de son navigateur, ces préférences seront réinitialisées.

---

## 📂 Structure des fichiers JSON de vocabulaire

L'application charge dynamiquement les données d'unités depuis le dossier `data/`. Chaque fichier JSON doit suivre cette structure :

```json
{
  "title": "EiM 9 - Unit 1",
  "words": [
    {
      "id": 1,
      "en": "cat",
      "spoken": "cat",
      "fr": "chat",
      "ipa": "kæt"
    },
    {
      "id": 2,
      "en": "read a book",
      "spoken": "read a book",
      "fr": "lire un livre",
      "ipa": "riːd ə bʊk"
    }
  ]
}
```

Chaque élément de la liste de mots contient les propriétés suivantes :

* **`id`** *(number)* : Identifiant unique du mot dans l'unité.
* **`en`** *(string)* : Texte affiché en anglais.
* **`spoken`** *(string, optionnel)* : Texte alternatif prononcé par la synthèse vocale (utile pour guider la prononciation si le texte affiché contient des annotations).
* **`fr`** *(string)* : Traduction en français.
* **`ipa`** *(string, optionnel)* : Transcription en alphabet phonétique international.

---

## 🛠️ Technologies utilisées

* **HTML5 / CSS3**
* **Tailwind CSS** (via CDN) pour le style et le design réactif.
* **JavaScript ES6+** (Vanilla JS)
* **Web Speech API** pour la synthèse vocale native des navigateurs.
* **Google Inter Font** pour la typographie.

---

## 🚀 Utilisation & Déploiement

1. Clonez ou téléchargez le dépôt.
2. Assurez-vous que vos fichiers de données d'unités sont placés dans un sous-dossier nommé `data/` (ex: `data/eim9_u1.json`).
3. Ouvrez `index.html` directement dans votre navigateur ou hébergez le projet sur n'importe quel serveur statique (GitHub Pages, Vercel, Netlify, etc.).



