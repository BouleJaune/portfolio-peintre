# Portfolio — Site de peintures

Site statique généré avec **Jekyll**, éditable via **Decap CMS**, hébergé sur **Netlify**.

---

## Architecture

```
portfolio-papa/
├── _config.yml           ← Config Jekyll (titre, email, etc.)
├── _data/site.yml        ← Données du site (modifiables via CMS)
├── _tableaux/            ← Un fichier .md par tableau
├── _layouts/             ← Templates HTML
├── _includes/            ← Header, footer
├── admin/
│   ├── index.html        ← Interface Decap CMS
│   └── config.yml        ← Config du CMS (champs, collections)
├── assets/
│   ├── css/style.css     ← Styles
│   └── images/           ← Photos des tableaux (uploadées via CMS)
├── index.html            ← Page d'accueil
├── galerie.html          ← Galerie complète
├── a-propos.md           ← Page à propos (éditable via CMS)
├── contact.html          ← Formulaire de contact
├── Gemfile               ← Dépendances Ruby
└── netlify.toml          ← Config Netlify
```

---

## Mise en place (30–45 min)

### 1. Créer le repo GitHub

```bash
git init
git add .
git commit -m "init"
gh repo create portfolio-papa --public --source=. --push
# ou via github.com → New repository → pousser manuellement
```

### 2. Déployer sur Netlify

1. Aller sur [app.netlify.com](https://app.netlify.com)
2. **Add new site → Import an existing project → GitHub**
3. Sélectionner le repo `portfolio-papa`
4. Les paramètres de build sont déjà dans `netlify.toml` → laisser par défaut
5. **Deploy site**

Le site sera disponible sur `https://xxxx.netlify.app`.
Optionnel : connecter un domaine personnalisé dans Site settings → Domain management.

### 3. Activer Netlify Identity + Git Gateway

Dans le dashboard Netlify :

1. **Site configuration → Identity** → Enable Identity
2. **Registration** → mettre sur **Invite only** (important !)
3. **Services → Git Gateway** → Enable Git Gateway
4. Revenir dans **Identity** → **Invite users** → saisir l'email de votre père
   - Il recevra un email d'invitation pour créer son mot de passe

### 4. Configurer Formspree (formulaire de contact)

1. Aller sur [formspree.io](https://formspree.io) → créer un compte gratuit
2. **New Form** → saisir l'email de destination
3. Copier l'ID de formulaire (ex : `xpzgkwqr`)
4. Dans `contact.html`, remplacer `YOUR_FORM_ID` :
   ```html
   action="https://formspree.io/f/xpzgkwqr"
   ```
5. Commit + push → Netlify rebuild automatiquement

### 5. Tester l'interface d'admin

1. Aller sur `https://votre-site.netlify.app/admin`
2. Se connecter avec les identifiants reçus par email
3. Vérifier que l'on peut créer un tableau, uploader une image, publier

---

## Utilisation par votre père

1. Aller sur `https://votre-site.netlify.app/admin`
2. Se connecter (email + mot de passe)
3. Cliquer **Tableaux → Nouveau tableau**
4. Remplir :
   - **Titre** (ex : *Lumière d'automne*)
   - **Image** → glisser-déposer ou choisir un fichier
   - **Technique** → menu déroulant
   - **Dimensions** (ex : `60 × 80 cm`)
   - **Année**
   - **Disponibilité**
   - **Description** (optionnel)
   - **Mettre en avant** (pour l'afficher sur la page d'accueil)
5. Cliquer **Publier**

→ Netlify reconstruit le site automatiquement (~1 min).

---

## Développement local

```bash
# Installer Ruby si nécessaire
brew install ruby  # macOS

# Installer les dépendances
bundle install

# Lancer le serveur local
bundle exec jekyll serve

# Ouvrir http://localhost:4000
```

---

## Personnalisation rapide

| Ce qu'on veut changer | Où |
|---|---|
| Nom, email, localisation | `_data/site.yml` ou CMS → Paramètres |
| Texte de la page À propos | CMS → Pages → À propos |
| Couleurs du site | `assets/css/style.css` → variables `:root` |
| Polices | `_layouts/default.html` → lien Google Fonts |
| Titre du navigateur | `_config.yml` → `title` |

---

## Notes

- **Gratuit** : Netlify free tier, GitHub free, Formspree 50 submissions/mois (gratuit)
- **Statique** : aucune base de données, aucun serveur à maintenir
- **Sauvegardé** : toutes les modifications passent par GitHub (historique complet)
- **Extensible** : on peut ajouter des pages, des collections, du multilingue
# portfolio-peintre
