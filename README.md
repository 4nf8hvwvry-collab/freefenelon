# Ressources communautaires

Recueil de ressources libres, publié sur https://4nf8hvwvry-collab.github.io/freefenelon/.

Tout le contenu de ce dépôt est placé dans le **domaine public** via [CC0 1.0](LICENSE) : vous pouvez le copier, le modifier, le redistribuer et l'utiliser, y compris à des fins commerciales, sans demander d'autorisation ni citer de source.

## Structure

```
.
├── site/                    Contenu publié (HTML, CSS, fichiers téléchargeables)
│   └── index.html
├── .github/workflows/       Publication automatique sur GitHub Pages
├── .githooks/               Contrôles locaux avant commit
├── LICENSE                  Texte officiel CC0 1.0
└── README.md
```

Seul le dossier `site/` est publié. Le reste du dépôt n'est pas visible en ligne.

## Publication

Chaque push sur `main` déclenche le workflow `.github/workflows/pages.yml`, qui :

1. supprime les métadonnées des fichiers publiés (images, PDF, documents bureautiques) avec `mat2` ;
2. publie le contenu de `site/` sur GitHub Pages.

Prérequis côté dépôt : **Settings > Pages > Source : GitHub Actions**, puis **Enforce HTTPS**.

Le workflow peut aussi être relancé à la main depuis l'onglet **Actions > Publication GitHub Pages > Run workflow**.

## Mise en place locale

Après le clone, activer les contrôles avant commit :

```bash
git config core.hooksPath .githooks
```

Le hook `pre-commit` bloque le commit si :

- l'adresse e-mail Git n'est pas une adresse `@users.noreply.github.com` ;
- la signature des commits est activée ;
- le fuseau horaire n'est pas UTC ;
- un fichier ajouté ou modifié contient des métadonnées identifiantes (auteur, GPS, appareil, logiciel), si `exiftool` est installé.

Outils conseillés sur macOS : `brew install exiftool mat2`.

Commande de commit recommandée :

```bash
TZ=UTC git commit -m "message"
```

## Ajouter une ressource

1. Déposer le fichier dans `site/` (ou un sous-dossier).
2. Nettoyer les métadonnées : `mat2 --inplace --lightweight site/chemin/fichier`.
3. Ajouter le lien dans `site/index.html`.
4. Committer et pousser.

Les contributions doivent être compatibles avec CC0 : ne déposez que des contenus dont vous êtes l'auteur ou qui sont déjà dans le domaine public.
