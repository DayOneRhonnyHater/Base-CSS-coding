# Notes techniques — pense-bête

Toutes les techniques CSS/HTML rencontrées dans les fichiers `exmp*`, regroupées ici pour s'y retrouver rapidement plus tard.

## Responsive / Media Queries

- **Approche "mobile first"** : on écrit d'abord les styles pour petit écran (sans `@media`), puis on ajoute des `@media (min-width: ...)` pour les écrans plus grands. Plus simple à maintenir que l'inverse.
- **Points de rupture (breakpoints) utilisés dans ces exemples :**
  - `480px` — téléphones en mode paysage
  - `600px` — début "tablette"
  - `768px–834px` — iPad en portrait (réglage précis avec `orientation: portrait`)
  - `1024px–1194px` — iPad en paysage (réglage précis avec `orientation: landscape`)
  - `1025px` — début "ordinateur"
  - `1440px` — très grands écrans
- `min-width` = "à partir de cette largeur". `max-width` = "jusqu'à cette largeur". On peut combiner les deux pour cibler une plage précise (ex : `min-width: 600px` et `max-width: 1024px` = uniquement les tablettes).
- `orientation: portrait` / `orientation: landscape` = cible le sens de l'écran (utile pour les tablettes qui changent beaucoup de proportions selon le sens).
- La balise `<meta name="viewport" content="width=device-width, initial-scale=1.0">` est **obligatoire** dans le `<head>` pour que les media queries fonctionnent correctement sur un vrai téléphone (sinon le téléphone affiche une version "zoomée" de la page desktop).

## Mise en page (Grid & Flexbox)

- **CSS Grid** (`display: grid`) : pour ranger des éléments en tableau (lignes + colonnes).
  - `grid-template-columns: 1fr` = 1 colonne qui prend toute la largeur
  - `grid-template-columns: repeat(3, 1fr)` = 3 colonnes égales
  - `gap` = espace entre les cases de la grille
- **Flexbox** (`display: flex`) : pour ranger des éléments en ligne (ou en colonne avec `flex-direction: column`).
  - `justify-content: space-between` = pousse les éléments aux deux extrémités
  - `justify-content: center` = centre les éléments
  - `align-items: center` = centre verticalement (si en ligne) ou horizontalement (si en colonne)
- Grid vs Flexbox en résumé : Grid pour une mise en page en 2 dimensions (lignes ET colonnes), Flexbox pour une seule dimension (soit une ligne, soit une colonne).

## Positionnement

- `position: static` = comportement normal, par défaut.
- `position: relative` = reste à sa place, mais sert de repère pour un enfant en `absolute`.
- `position: absolute` = sort du flux normal, se positionne par rapport au parent le plus proche en `relative`/`absolute`/`fixed`.
- `position: fixed` = reste à un endroit précis de l'écran, même si on scrolle.
- `position: sticky` = reste normal jusqu'à ce qu'on scrolle jusqu'à lui, puis se colle (utilisé sur le `<header>` de exmp3).
- `z-index` = gère l'empilement quand plusieurs éléments se chevauchent (plus haut = plus proche de l'utilisateur, donc au-dessus visuellement). Ne fonctionne que sur les éléments qui ont un `position` autre que `static`.

## Variables CSS (`:root` + `var()`)

- Déclarées une fois dans `:root{ --nom-variable: valeur; }`, réutilisées partout avec `var(--nom-variable)`.
- Change UNE valeur à un seul endroit au lieu de la chercher dans tout le fichier (utilisé massivement dans exmp3.css pour les couleurs, ombres, rayons d'arrondi).

## Effets visuels

- `box-shadow: décalage-x décalage-y flou couleur` = ombre portée. Une ombre "légère" (`shadow-sm`) et une "grosse" (`shadow-md`) sont souvent combinées pour un effet de profondeur qui s'accentue au survol.
- `transition: propriété durée` = anime le changement d'une propriété (couleur, position, ombre...) au lieu que ce soit instantané. Utilisé avec `:hover`.
- `transform: translateY(-6px)` = déplace un élément verticalement sans affecter les autres éléments autour (contrairement à `margin`). Utilisé pour l'effet "la carte flotte" au survol.
- `linear-gradient(angle, couleur1, couleur2)` = fond en dégradé entre deux couleurs.
- `backdrop-filter: blur(8px)` = floute ce qu'il y a DERRIÈRE un élément (effet "verre dépoli"), utilisé sur le header sticky.
- `border-radius: 50%` sur un élément carré (même largeur/hauteur) = cercle parfait (utilisé pour les avatars et icônes rondes).
- `scroll-behavior: smooth` (sur `html`) = fait défiler la page en douceur quand on clique sur un lien `#ancre` au lieu de sauter brutalement.

## Polices (`@font-face`)

- `font-display: swap` = affiche un texte de secours immédiatement, puis bascule vers la police personnalisée dès qu'elle est chargée (évite le texte invisible pendant le chargement).
- Une police avec plusieurs graisses/styles = plusieurs blocs `@font-face` séparés (un par combinaison poids/style), le navigateur choisit automatiquement le bon fichier selon `font-weight`/`font-style` demandés dans le CSS.
- Police **variable** : un seul fichier, une plage de graisses déclarée avec `font-weight: 100 900`, puis n'importe quel chiffre entre les deux fonctionne.
- `src: local('NomPolice')` = vérifie si la police est déjà installée sur l'appareil avant de télécharger quoi que ce soit.
- `@import url(...)` pour charger une police externe doit être **tout en haut** du fichier CSS pour fonctionner ; une balise `<link>` dans le HTML est généralement préférable (chargement plus rapide, en parallèle).
- Liste de polices "système" (`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto...`) = zéro téléchargement, apparence légèrement différente selon l'OS.

## Menu mobile ("hamburger")

Pattern utilisé dans tous les exemples :
```html
<button onclick="document.querySelector('nav').classList.toggle('open')">☰</button>
```
Le bouton ajoute/enlève la classe CSS `open` sur `<nav>`. C'est cette classe qui déclenche l'ouverture/fermeture visuelle (via `display`, ou via un `right`/`transform` animé dans exmp3). Sur ordinateur, on cache le bouton (`display: none`) et on affiche le menu directement en ligne.

## Pièges / choses à surveiller

- `box-sizing: border-box` (mis sur `*` en début de fichier) évite que le `padding`/`border` agrandissent la taille totale d'un élément au-delà de sa `width` définie — presque toujours utile de le mettre par défaut.
- Un `<link href="...">` ou un `src="fonts/..."` qui pointe vers un fichier qui n'existe pas ne fait pas planter la page : le navigateur ignore silencieusement et retombe sur le style/police de secours suivant dans la liste. Utile pour prototyper, mais peut cacher un vrai oubli de fichier en production.
- Après avoir renommé un fichier `.html`/`.css`, il faut penser à vérifier/mettre à jour manuellement les `<link>`, les `<title>`, et les chemins d'images à l'intérieur — le renommage du fichier ne met pas à jour son contenu.
