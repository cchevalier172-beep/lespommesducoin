# Design System — Les Pommes du Coin

Design tokens et patterns pour créer des pages cohérentes avec le site existant.

## Principe

Direction visuelle : **carnet de route / rural contemporain**. Chaleureux, sobre, ni corporate, ni startup. On reste sur du crème, du vert profond, du granit et une touche d'ocre. Pas de fond sombre qui masque le contenu, pas d'angles agressifs.

## Couleurs

Définies dans `src/styles/global.css` via `@theme` Tailwind. Utiliser les tokens, jamais les hex bruts.

| Token | Hex | Usage |
|---|---|---|
| `cream` | `#f5f0eb` | Fond clair principal, texte sur fond vert/granit |
| `granit` | `#2c2c2a` | Texte principal, sections sombres (itinéraire, footer) |
| `vert` | `#2d5a27` | Accent principal, badges, boutons d'écoute |
| `vert-fonce` | `#183a19` | Dégradés hero, fond carte itinéraire |
| `vert-moyen` | `#214a21` | Dégradés hero |
| `ocre` | `#b87c4b` | Accent secondaire, étiquettes de section, CTA principal |
| `ocre-clair` | `#e5b98b` | Surlignage hover, titres sur fond sombre |
| `ocre-fonce` | `#cf9160` | Hover du CTA principal |
| `beige` | `#e8dfd3` | Fond de section À propos |
| `beige-moyen` | `#d9cfbf` | Placeholder image épisodes |
| `gris` | `#5f5d58` | Texte secondaire |
| `gris-clair` | `#77736d` | Textes tertiaires (lieux, numéros) |
| `blanc-ocre` | `#eed7bd` | Eyebrow du hero |

Opacités utilisées : `cream/90`, `cream/70`, `cream/65`, `cream/45`, `granit/85`, `granit/15`, `white/15`, `white/20`, `white/25`, `white/45`.

## Typographie

Chargées via Google Fonts dans `BaseLayout.astro`.

| Rôle | Famille | Usage |
|---|---|---|
| `font-serif` | Fraunces | Titres, grandes citations, nom du podcast |
| `font-sans` | DM Sans | Corps de texte, navigation, boutons |
| `font-mono` | DM Mono | Numéros d'épisodes (E01, E02...) |

**Règles :**
- Titres en `font-serif`, `tracking-tight`, `leading-tight`
- Eyebrow (étiquette de section) : `text-xs font-medium uppercase tracking-[0.16em] text-ocre`
- Corps : `text-base leading-relaxed text-gris`
- Ne jamais utiliser `font-sans` pour un titre, ni `font-serif` pour du corps long.

## Espacements

- **Container maxi** : `max-w-7xl` avec `px-5 sm:px-8 lg:px-12`
- **Vertical sections** : `py-20 md:py-28` (plus léger : `py-16`)
- **Écart entre un eyebrow et un titre** : `mt-4` / `mt-5`
- **Écart entre un titre et un paragraphe** : `mt-6` / `mt-7`
- **Grille desktop** : `md:grid-cols-12` avec colonnes à `md:col-span-*` et `md:col-start-*`
- **Bordure séparatrice** : `border-b border-granit/15`

## Patterns récurrents

### Section standard
```astro
<section id="..." class="mx-auto max-w-7xl px-5 py-20 sm:px-8 md:py-28 lg:px-12">
  <p class="text-xs font-medium uppercase tracking-[0.16em] text-ocre">Eyebrow</p>
  <h2 class="mt-4 text-4xl tracking-tight sm:text-5xl font-serif">Titre</h2>
  <p class="mt-6 max-w-xl text-base leading-relaxed text-gris">Texte</p>
</section>
```

### Section sombre
Fond `bg-granit` (ou `bg-vert-fonce` pour un encart) + texte `text-cream`, eyebrow `text-ocre-clair`, paragraphes `text-cream/70`.

### Bouton principal (CTA)
```astro
<a href="#" class="inline-flex items-center gap-3 bg-ocre px-6 py-4 text-sm font-medium text-white transition hover:bg-ocre-fonce">
```

### Bouton fantôme
```astro
<a href="#" class="inline-flex items-center gap-2 border border-cream/60 px-4 py-2.5 text-xs font-medium uppercase tracking-[0.12em] transition hover:bg-cream hover:text-vert">
```

### Lien d'écoute (épisode)
```astro
<a href="#" class="inline-flex items-center gap-2 text-sm font-medium text-vert transition hover:text-ocre">
  Écouter
  <span class="flex h-9 w-9 items-center justify-center rounded-full border border-vert">
    <iconify-icon icon="solar:play-linear" width="16" stroke-width="1.5"></iconify-icon>
  </span>
</a>
```

## Icônes

Icônes via **Iconify** (solar, `stroke-width="1.5"`), chargées dans `BaseLayout.astro` :
- Logo / pomme : `solar:apple-linear`
- Lecture : `solar:play-linear`, `solar:play-circle-linear`
- Carte : `solar:map-point-linear`
- Micro : `solar:microphone-3-linear`
- Plateformes : `solar:headphones-round-linear`, `solar:podcast-linear`, `solar:link-round-linear`

## Composants existants

Tous dans `src/components/` :

| Composant | Rôle | Props |
|---|---|---|
| `Header.astro` | Navigation | — |
| `Hero.astro` | En-tête plein écran (inclut Header) | — |
| `Contexte.astro` | Texte de cadrage "point de départ" | — |
| `Galerie.astro` | Bloc photos du trajet (2 images + 1 grande) | — |
| `Itineraire.astro` | Section sombre carte SVG + étapes | — |
| `Episodes.astro` | Section épisodes, compose `EpisodeCard` | — |
| `EpisodeCard.astro` | Un épisode réutilisable | `numero`, `lieu`, `badge`, `titre`, `description`, `imageSrc?`, `imageAlt?`, `placeholderIcon?`, `placeholderLabel?`, `bordered?` |
| `APropos.astro` | Section À propos | — |
| `Credits.astro` | Crédits 3 colonnes | — |
| `Footer.astro` | Pied de page + liens plateformes | — |

## Ajouter une page

1. Copier `index.astro` comme base (layout + imports).
2. Réutiliser les composants existants ; pour une nouvelle section, suivre les patterns ci-dessus.
3. Pour de nouvelles images : les déposer dans `public/images/` et référencer `/images/nom.jpg`.
4. Mettre à jour `BaseLayout.astro` pour le `<title>` et la meta description.
