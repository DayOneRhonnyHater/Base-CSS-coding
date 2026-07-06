# Base-CSS-coding

Un ensemble d'exemples pour apprendre le CSS responsive (adapté à toutes les tailles d'écran), les polices d'écriture, et la construction d'une page complète.

## exmp1 — Grille responsive de base

**Fichiers :** [exmp1.html](exmp1.html) + [exmp1.css](exmp1.css)

Une démo simple qui montre comment une grille de cartes s'adapte automatiquement à la largeur de l'écran :

- Téléphone (< 480px) : 1 colonne
- Téléphone en paysage (≥ 480px) : 2 colonnes
- Tablette / iPad (600px – 1024px) : 3 colonnes, avec des réglages précis pour le portrait (768–834px) et le paysage (1024–1194px) de l'iPad
- Ordinateur (≥ 1025px) : 4 colonnes
- Très grand écran (≥ 1440px) : titres encore plus grands, largeur max augmentée

Contient aussi : un menu mobile caché par défaut qui s'ouvre avec un bouton "hamburger" (☰), et qui redevient un menu horizontal normal sur tablette/ordinateur.

> ⚠️ Ce fichier HTML pointe encore vers `exmp2.css` dans son `<link>` (reste d'un renommage). Dites-moi si vous voulez que je corrige le lien vers `exmp1.css`.

## exmp2 — Intégration de polices (`@font-face`)

**Fichier :** [exmp2.css](exmp2.css) *(fichier de référence, sans page HTML associée pour l'instant)*

Regroupe les différentes façons d'ajouter des polices personnalisées à un projet :

1. `@font-face` basique avec un fichier hébergé par vous (woff2 + woff)
2. Plusieurs graisses/styles (normal, gras, italique, gras-italique) via plusieurs blocs `@font-face`
3. Police "variable" : un seul fichier qui couvre toute une plage de graisses (`font-weight: 100 900`)
4. `local()` : vérifie si la police est déjà installée sur l'appareil avant de la télécharger
5. `@import` depuis un service comme Google Fonts (alternative à la balise `<link>`)
6. Liste de polices "système" : aucune police téléchargée, on utilise celle déjà installée sur l'ordinateur/téléphone

> Note : les fichiers de police référencés (`fonts/MyCustomFont.woff2`, etc.) n'existent pas réellement sur le disque — c'est un exemple pédagogique, le navigateur retombera simplement sur les polices de secours (Arial, Georgia...).

## exmp3 — Page complète "Nova" (landing page)

**Fichiers :** [exmp3.html](exmp3.html) + [exmp3.css](exmp3.css) + [exmp3.md](exmp3.md)

Un exemple abouti de page d'accueil, avec un vrai système de design (variables CSS pour les couleurs, ombres, arrondis...) :

- En-tête collant (`sticky`) avec menu qui glisse depuis la droite sur mobile, et devient une barre horizontale sur ordinateur
- Section d'accueil ("hero") avec dégradé de couleur et boutons d'action
- Grille de 3 cartes "pourquoi nous choisir"
- Section "à propos" avec image + texte côte à côte
- Témoignages clients avec avatars (initiales dans un rond coloré)
- Bandeau d'appel à l'action (fond foncé)
- Pied de page à 4 colonnes

Le fichier [exmp3.md](exmp3.md) documente chaque section avec son code et des captures d'écran.

> ⚠️ Ce fichier HTML pointe encore vers `exmp5.css` dans son `<link>` (reste d'un renommage) — ce fichier n'existe plus, il faudrait corriger vers `exmp3.css`.

## Autre fichier

- [NOTES.md](NOTES.md) — un pense-bête technique qui regroupe toutes les propriétés/astuces CSS utilisées dans ces exemples, utile si vous voulez comprendre ou réutiliser une technique précise plus tard.
