# Bass-Cour — Site vitrine d’un festival électronique

Projet réalisé dans le cadre du module CSS avancé. Bass-Cour est un festival fictif organisé les **18 et 19 juin 2027**, à la **Ferme des Silos, à Arras**. Son identité associe une ambiance agricole, des titres condensés et une palette crème, noir et vert électrique.

> Les chemins ci-dessous sont relatifs à ce dossier, qui contient `index.html` et `css/`. Pour le dépôt final, ce document est à renommer `README.md`.

## Groupe

| Information | Valeur |
|---|---|
| Nom du groupe | |
| Membres et rôles référents | Alexandre LEGRAND, dev |
| Événement / thème | Bass-Cour — festival de musique électronique en plein champ |
| Lien du dépôt Git | |
| Convention de nommage | BEM : `.site-header`, `.card__visual`, `.card__visual--01` ; préfixe `u-` pour les classes utilitaires. |

## Ouvrir le projet

Ouvrir directement `index.html` dans un navigateur récent. Aucune compilation, installation de dépendances ou commande de démarrage n’est nécessaire. Les images et les polices sont chargées depuis des services externes : leur affichage nécessite un accès à Internet.

La page comprend un en-tête avec navigation, un hero, un programme sur deux jours, six cartes artistes, un bandeau mettant un artiste à l’affiche, trois offres de pass, une FAQ et un pied de page. Les tarifs sont de 39 €, 69 € et 99 €. Les boutons de demande de pass conduisent au contact du festival fictif.

## Organisation des fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | Structure sémantique, contenus, navigation et interactions HTML natives. |
| `css/main.css` | Point d’entrée CSS, ordre des layers et imports. |
| `css/reset.css` | Normalisation des styles du navigateur. |
| `css/tokens.css` | Palette et échelles primitives, puis rôles sémantiques, tailles fluides et thèmes. |
| `css/base.css` | Styles par défaut des éléments HTML : textes, titres, liens, contrôles et focus. |
| `css/layout.css` | Mise en page, grilles, Flexbox et adaptations mobile/desktop. |
| `css/components.css` | Apparence des composants, états interactifs, container queries et animations. |
| `css/utilities.css` | Texte visuellement masqué et neutralisation des mouvements selon la préférence utilisateur. |

## Localisation des exigences

| Exigence | Élément attendu | Fichier:ligne | Commentaire |
|---|---|---|---|
| 1. Architecture | Ordre des layers | `css/main.css:16` | Ordre déclaré une seule fois : `reset, base, layout, components, utilities`. Les règles sont placées dans leur layer. |
| 1. Architecture | Tokens primitifs | `css/tokens.css:6`, `css/tokens.css:20` | Échelle d’espacements et palette brute, par exemple `--space-1` et `--color-cream-100`. |
| 1. Architecture | Tokens sémantiques | `css/tokens.css:31` | Les rôles tels que `--color-surface` référencent la palette. Les composants consomment les rôles plutôt que les couleurs primitives. |
| 1. Architecture | Nesting natif | `css/components.css:32` | États des liens imbriqués dans le header avec `& a` puis `&:hover`, sans préprocesseur. |
| 2. Mise en page | Grille à zones nommées | `css/layout.css:22` | Le programme passe de `titre / jour1 / jour2` en une colonne à deux journées côte à côte dès 48rem. |
| 2. Mise en page | Subgrid | `css/layout.css:295`, `css/layout.css:308` | Chaque élément de liste et chaque carte partagent quatre pistes : visuel, en-tête, bio et détails. Les contenus restent alignés malgré des biographies de longueurs différentes. |
| 2. Mise en page | Flexbox | `css/layout.css:58`, `css/layout.css:117` | Header et groupe de boutons du hero : alignements, `gap` et changement de direction selon la largeur. |
| 3. Responsive | Mobile-first | `css/layout.css:32` | Styles initiaux pour petits écrans ; media queries ascendantes en `width >=`. Le programme s’élargit à 48rem, le header affiche sa navigation desktop à 64rem. |
| 3. Responsive | Typographie fluide | `css/tokens.css:49` | Tailles du corps et des titres en `clamp()`, avec des valeurs minimales et maximales. |
| 3. Responsive | Container query et deux contextes | `css/layout.css:283`, `css/layout.css:373`, `css/components.css:851`, `css/components.css:961` | Conteneurs nommés `artist-card` sur la grille et sur le bandeau « À l’affiche ». Typographie adaptée dès 40rem ; carte du bandeau horizontale dès 28rem de largeur disponible. |
| 3. Responsive | Robustesse à 320px | `css/layout.css:285`, `css/layout.css:310`, `css/layout.css:315` | Colonnes `minmax(0, 1fr)`, largeur minimale nulle et hauteur réservée au visuel. Aucun débordement horizontal relevé dans les tests responsive. |
| 4. Sélecteurs | `:has()` pertinent | `css/components.css:581` | L’offre contenant `.offer__badge` reçoit automatiquement le fond vert et les couleurs de mise en avant. |
| 4. Sélecteurs | `:where()` et `:is()` | `css/base.css:27`, `css/components.css:882` | `:where()` factorise les titres avec une spécificité nulle ; `:is()` regroupe les éléments animés du hero. |
| 5. Thème | `light-dark()` et `color-scheme` | `css/tokens.css:31`, `css/tokens.css:251` | Les couleurs sémantiques dépendent du thème calculé. Le thème initial est clair ; les éléments natifs suivent `color-scheme`. |
| 5. Thème — bonus | Bascule CSS-only | `index.html:25`, `css/tokens.css:255` | La case à cocher est détectée par `:root:has(#theme-toggle:checked)` et active `color-scheme: dark`. |
| 6. Animations | Transition n°1 | `css/components.css:866` | Boutons : transitions ciblées sur le déplacement et les couleurs, avec durées et courbes issues des tokens. |
| 6. Animations | Transition n°2 | `css/components.css:496` | FAQ : transition des couleurs au survol ; l’indicateur plus/moins évolue à l’ouverture. |
| 6. Animations | Keyframes | `css/components.css:882`, `css/components.css:927` | `bass-entrance` fait apparaître les contenus du hero progressivement, avec un léger déplacement et une variation d’opacité. |
| 6. Animations | Réduction des mouvements | `css/utilities.css:24`, `css/utilities.css:36` | Le dernier layer neutralise animations, transitions et défilement fluide, sans `!important`. Les déplacements au survol sont aussi neutralisés. |
| 6. Animations — bonus | Popover animé | `index.html:31`, `css/components.css:902` | Menu mobile natif avec `popover` et `popovertarget`. Animation d’entrée seulement lorsque les mouvements sont acceptés. |
| 7. Accessibilité | Landmarks et hiérarchie | `index.html:14`, `index.html:43`, `index.html:47`, `index.html:272` | `lang="fr"`, header/nav/main/footer, un seul h1, sections titrées et sous-titres h3. |
| 7. Accessibilité | Focus clavier | `css/base.css:190`, `css/components.css:522` | Contour visible au clavier, vert sur les surfaces sombres ; contour intérieur sur les questions de FAQ. |
| 7. Accessibilité | Contrastes des couleurs unies | `css/tokens.css:20`, `css/tokens.css:31` | Calcul de luminance relative sRGB : crème/noir 15,85:1 ; crème/olive 7,33:1 ; vert/noir 14,40:1 ; crème/fond de bouton au survol 6,01:1. Ces paires dépassent 4,5:1. Ce contrôle ne constitue pas une certification de tous les états ni des textes sur photo. |
| 7. Accessibilité | Alternatives des visuels | `index.html:86` | Les portraits sont des backgrounds sur des éléments `role="img"` avec un `aria-label` descriptif. Il n’y a pas de balise img nécessitant un attribut alt dans cette version. |
| 7. Accessibilité | Libellés complémentaires | `css/utilities.css:11`, `index.html:94` | `.u-visually-hidden` conserve le nom de l’artiste pour les lecteurs d’écran dans les contrôles « En savoir plus ». |
| 8. Qualité | Résultat du validateur W3C | | |
| 8. Qualité | Absence de `!important` | `css/utilities.css:24` | Aucune déclaration `!important`. La priorité du layer utilities suffit à respecter la réduction des mouvements. |

## Choix techniques

Grid organise les éléments en deux dimensions : les journées, les offres de pass et les cartes artistes. Flexbox sert aux groupes principalement linéaires, notamment la navigation et les boutons. Le subgrid aligne les quatre parties des cartes sur les pistes communes à leur ligne.

Le conteneur de la grille des artistes est placé sur la liste, et non sur ses éléments subgrid : les tests ont montré que le confinement de mise en page des conteneurs individuels empêchait ces éléments de partager correctement leurs pistes. Le bandeau « À l’affiche » utilise un conteneur distinct et montre la réutilisation de la même carte avec une autre largeur disponible.

Le thème est géré sans JavaScript. La case à cocher modifie le `color-scheme` de la racine ; les couleurs `light-dark()` choisissent alors leur valeur claire ou sombre. Le choix n’est pas enregistré entre les visites.

Le menu utilise la Popover API, et la FAQ ainsi que les détails artistes utilisent `details`/`summary`. Les interactions restent disponibles sans animation. Les animations n’ont pas de boucle permanente et n’interviennent pas dans le calcul des dimensions des composants.

## Vérifications réalisées

Contrôles effectués pendant le développement avec des navigateurs automatisés et des outils locaux de validation.

| Contrôle | Résultat |
|---|---|
| Chrome, Edge et Firefox | Largeurs de 320, 375, 768, 1024 et 1440px, en thèmes clair et sombre : 30 cas sans débordement horizontal ni chevauchement entre visuel et nom d’artiste. |
| Menu mobile | Ouverture et fermeture par Échap vérifiées dans les trois navigateurs ; bouton burger masqué aux largeurs desktop testées. |
| FAQ | Ouverture native vérifiée dans les trois navigateurs. |
| Clavier | Parcours par Tab, accès au menu et ouverture des détails par Entrée vérifiés dans Chrome et Firefox. |
| Réduction des mouvements | Aucune animation ni transition calculée en mode reduce dans les trois navigateurs ; contenu du hero toujours visible. |
| Subgrid | Positions des en-têtes, biographies et détails alignées entre les cartes d’une même ligne, même lorsqu’un détail est ouvert. |
| Agrandissement | Zoom CSS à 200 % sans débordement dans les trois navigateurs ; viewport réduit à 720px également contrôlé. Le zoom natif du navigateur n’a pas été vérifié par cette automatisation. |
| HTML | Aucune erreur au contrôle local avec html-validate, avec certaines règles de convention désactivées, notamment les rôles list explicites du starter et le style des éléments vides. |
| CSS | Les sept feuilles sont analysées sans erreur de syntaxe par css-tree. |
| Contrôles de cohérence | Aucun token référencé manquant, aucun identifiant dupliqué et aucune référence interne absente. Nesting limité à trois niveaux. |

La validation publique W3C n’a pas été effectuée. Les validations locales ci-dessus ne remplacent pas ce contrôle.

## Avertissements du validateur W3C non corrigés

| Fichier:ligne | Message du validateur | Pourquoi c’est valide |
|---|---|---|
| | | |

## Bonus techniques présentés

| Fonctionnalité | Fichier:ligne | Explication et comportement sans animation |
|---|---|---|
| Bascule de thème CSS-only | `css/tokens.css:255` | Le sélecteur relationnel has détecte l’état de la case à cocher et change le thème sans script. |
| Popover natif animé | `index.html:31`, `css/components.css:902` | Le navigateur gère l’ouverture et la fermeture du menu. Sans animation, le menu reste immédiatement utilisable. |

## JavaScript

Aucun JavaScript n’est utilisé dans le site. Aucun framework CSS, préprocesseur ou outil de compilation n’est nécessaire. Les scripts de test utilisés pendant le développement ne sont pas chargés par la page.

## Déclaration d’usage d’outils d’IA

| Outil | Utilisation | Parties concernées |
|---|---|---|
| Codex | Compléter la structure HTML à partir de la maquette fournie et proposer des contenus fictifs. | `index.html` |
| Codex | Construire progressivement les styles, les tokens, les adaptations responsive, les thèmes et les animations. | Fichiers du dossier `css/` |
| Codex | Expliquer le thème sans JavaScript et la cascade des layers ; corriger les problèmes de visuels et de subgrid ; comparer le projet à l’énoncé et au barème. | HTML et CSS |
| Codex | Réaliser des vérifications automatisées et compléter ce document à partir du code et des contrôles effectués. | Tests de développement et `README_rendu.md` |

## Qui a fait quoi

| Membre | Principales contributions |
|---|---|
| | |
| | |
| | |

## Crédits

Les crédits sont également accessibles dans le footer, à partir de `index.html:289`. Les liens des images ont été repris depuis Google Images et les services indiqués ci-dessous. Les champs de licence non renseignés restent à compléter.

### Polices et éléments graphiques

| Ressource | Source | Licence |
|---|---|---|
| Barlow Condensed | [Google Fonts — fichier de licence](https://github.com/google/fonts/blob/main/ofl/barlowcondensed/OFL.txt) | SIL Open Font License 1.1 |
| Space Grotesk | [Google Fonts — fichier de licence](https://github.com/google/fonts/blob/main/ofl/spacegrotesk/OFL.txt) | SIL Open Font License 1.1 |
| Icônes calendrier et enveloppe | SVG en ligne réalisés pour ce projet | |
| Hachures, repères de lieu, étiquettes et encoches des billets | Dessins réalisés en CSS pour ce projet | |
| Maquette desktop et mobile | Maquette fournie pour le projet | |

### Images

| Visuel | Source utilisée | Licence |
|---|---|---|
| Grange du hero | Vecteezy — URL dans `css/components.css:158` et crédit dans le footer | |
| DJ GOATESQUE | Miniature utilisée via Google Images — `.card__visual--01` | |
| S.H.E.E.P | Magnific / Freepik — `.card__visual--02` | |
| Le Buffle | Miniature utilisée via Google Images — `.card__visual--03` | |
| Capitaine Coq | Miniature utilisée via Google Images — `.card__visual--04` | |
| Peppa | Magnific / Freepik — `.card__visual--05` | |
| Pachyderme | Miniature utilisée via Google Images — `.card__visual--06` | |
