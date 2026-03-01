# NASA Image Explorer

Application web permettant de rechercher et d’afficher dynamiquement des images issues de l’API publique de la NASA.
Les résultats sont présentés sous forme d’un bloc principal et de trois blocs secondaires avec gestion d’aperçu des descriptions.

## Fonctionnalités

- Recherche dynamique via formulaire
- Appel à l’API NASA (fetch)
- Affichage de 4 résultats :
    1 résultat principal (mis en avant)
    3 résultats secondaires

- Gestion du texte long avec bouton “Lire plus / Réduire”
- Loader animé pendant le chargement
- Gestion simple des erreurs réseau

## Logique Générale
### Sélection des éléments DOM

Le script commence par récupérer les éléments nécessaires :

form → gestion de la recherche

main → conteneur des résultats

pulse-loader → animation de chargement

Blocs principaux et secondaires (images, titres, descriptions)

Boutons “Lire plus”

### Requête API

**La fonction générique :**

fetchObject(url, options, callback)

Envoie une requête fetch

Transforme la réponse en JSON

Appelle une fonction callback avec les données

Gère les erreurs (affiche le contenu même en cas d’erreur et masque le loader)

️### Traitement des données

Les données récupérées suivent la structure de l’API NASA :

data.collection.items

Trois fonctions principales exploitent ces données :

**recoltImage(groupData)**

Récupère les URLs des images

Met à jour les attributs src

**recoltTitle(groupData)**

Récupère les titres

Met à jour les contenus textuels

**recoltDescription(groupData)**

Récupère les descriptions

Active le système de lecture étendue

### Système "Lire plus"

**Fonction :**

setupToggle(btn, textEl, fullText, previewLength)

**Fonctionnement :**

Affiche un extrait du texte (150 caractères)

Alterne entre :

Texte réduit

Texte complet

Change dynamiquement le texte du bouton

### Cycle d’exécution

- L’utilisateur soumet le formulaire

- L’URL est construite dynamiquement avec encodeURIComponent

- Appel API via fetchObject

- Traitement des données avec recoltData

- Affichage des résultats

- Masquage du loader

### Structure des Objets Internes

Le script utilise trois objets pour stocker temporairement les données :

img = {
  imgBig,
  img1,
  img2,
  img3
}

title = {
  titleBig,
  title1,
  title2,
  title3
}

description = {
  descriptionBig,
  description1,
  description2,
  description3
}


### Points d’amélioration envisageables

- Vérifier la présence des propriétés avant accès (optional chaining)

- Gérer les cas où moins de 4 résultats sont retournés

- Ajouter gestion des erreurs utilisateur (ex: recherche vide)

- Implémenter un système de pagination

- Ajouter un message si aucun résultat trouvé

- Nettoyer les anciens événements avant nouveau fetch

*Exemple d’URL API*
https://images-api.nasa.gov/search?media_type=image&q=mars

### Licence

Projet éducatif utilisant l’API publique NASA.
