# Les Pommes du Coin — Site

Mini-série podcast. Site statique Astro + Tailwind, déployé sur Cloudflare Pages.

## Développement

```bash
npm install
npm run dev
```

## Build

```bash
npm run build
```

Les fichiers sont générés dans `dist/`.

## Déploiement Cloudflare Pages

### Option 1 : liaison Git (recommandée, déploiement auto à chaque push)

1. Créer un repo GitHub avec ce dossier.
2. Dans le dashboard Cloudflare → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
3. Choisir le repo et configurer :

   - **Framework preset** : Astro
   - **Build command** : `npm run build`
   - **Build output directory** : `dist`
   - **Environment variables** : aucune

4. Déployer. À chaque `git push`, Cloudflare Pages reconstruit et redéploie automatiquement.

### Option 2 : déploiement manuel via wrangler

```bash
npx wrangler pages deploy dist --project-name=les-pommes-du-coin
```

## Structure

```
src/
├── layouts/BaseLayout.astro   # Layout racine (head, polices, body)
├── pages/index.astro          # Page d'accueil (la landing complète)
└── styles/global.css          # Tailwind + variables de thème (couleurs Limousin)
public/
└── images/                    # Photos locales (à y déposer)
```

## Images

Le site utilise actuellement des images placeholder (Unsplash). Pour les photos du voyage et les portraits de Marie et Mathilde, déposer les fichiers dans `public/images/` puis remplacer les `src` correspondants dans `src/pages/index.astro` par des chemins locaux (`/images/marie.jpg`, etc.).
