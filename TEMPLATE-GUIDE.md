# Guide des Templates

Ce guide vous explique comment créer, modifier, et maintenir des templates dans ce projet.

## 📋 Table des matières

- [Qu'est-ce qu'un template ?](#quest-ce-quun-template-)
- [Créer un nouveau template](#créer-un-nouveau-template)
- [Structure d'un template](#structure-dun-template)
- [Modifier un template existant](#modifier-un-template-existant)
- [Extraire des composants réutilisables](#extraire-des-composants-réutilisables)
- [Bonnes pratiques](#bonnes-pratiques)
- [Checklist de qualité](#checklist-de-qualité)
- [Contribuer un template](#contribuer-un-template)

## Qu'est-ce qu'un template ?

Un **template** dans ce projet est une **page HTML complète** qui :

✅ Utilise **Tailwind CSS** pour le styling
✅ Suit le **design system** documenté dans `.context/`
✅ Est **accessible** (WCAG AA minimum)
✅ Est **responsive** (mobile → desktop)
✅ Inclut une **documentation** claire
✅ Contient des **composants extraits** réutilisables

### Templates existants

- **`dashboard-modern/`** - Dashboard analytique moderne avec graphiques
- **`landing-page-fintech/`** - Landing page pour applications fintech
- **`dashboard-leads/`** - Dashboard de gestion de leads

Explorez ces templates pour comprendre les patterns.

## Créer un nouveau template

### Méthode 1 : Avec Claude Code (Recommandé)

C'est la méthode la plus rapide et cohérente.

#### Étape 1 : Définir votre template

Réfléchissez à :
- **Type** : Landing page, dashboard, blog, e-commerce, etc.
- **Sections** : Quelles sections principales ?
- **Fonctionnalités** : Interactivité, graphiques, formulaires ?
- **Public cible** : SaaS, fintech, e-commerce, etc.

#### Étape 2 : Prompt à Claude Code

```
Crée un nouveau template [TYPE] dans le dossier [nom-du-template]/

Structure :
[Listez les sections principales]

Fonctionnalités :
[Listez les fonctionnalités]

Exigences :
- Suis le design system dans .context/
- Accessible WCAG AA
- Responsive mobile-first
- Utilise Alpine.js pour l'interactivité si nécessaire
- Inclut des commentaires de section clairs

Après la création :
1. Génère le fichier principal index.html
2. Crée un README.md pour le template
3. Extrait les composants réutilisables dans components/
4. Liste les dépendances et instructions d'utilisation
```

**Exemple concret :**

```
Crée un nouveau template Blog dans le dossier blog-modern/

Structure :
- Header avec navigation sticky
- Hero section avec featured post grand format
- Grille de posts (3 colonnes desktop, 1 mobile)
- Sidebar avec catégories et posts populaires
- Newsletter signup section
- Footer

Fonctionnalités :
- Filtrage par catégories (Alpine.js)
- Recherche de posts
- Pagination
- Temps de lecture sur chaque post
- Tags/catégories

Exigences :
- Suis le design system dans .context/
- Accessible WCAG AA
- Responsive mobile-first
- Utilise Alpine.js pour le filtrage et recherche
- Inclut des commentaires de section clairs

Après la création :
1. Génère index.html
2. Crée README.md
3. Extrait les composants (PostCard, CategoryFilter, Sidebar)
4. Liste les dépendances
```

#### Étape 3 : Révision et ajustements

```
# Après génération, testez et ajustez :

"Ajoute un mode dark mode à ce template"
"Améliore les animations d'apparition au scroll"
"Rends la sidebar collapsible sur mobile"
```

#### Étape 4 : Documentation et assets

```
"Crée un fichier preview.png placeholder pour le screenshot"
"Ajoute des instructions de personnalisation dans le README"
"Liste toutes les classes Tailwind customisées utilisées"
```

### Méthode 2 : Manuellement

Si vous préférez coder manuellement :

#### Étape 1 : Créer la structure

```bash
# Créer le dossier du template
mkdir nom-du-template
cd nom-du-template

# Créer les fichiers de base
touch index.html
touch README.md
mkdir components
```

#### Étape 2 : Créer index.html

```html
<!DOCTYPE html>
<html lang="fr" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nom du Template</title>
    <meta name="description" content="Description du template">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <!-- Alpine.js (si nécessaire) -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

    <!-- Configuration Tailwind personnalisée -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        // Référez-vous à .context/styling/design-system.md
                    }
                }
            }
        }
    </script>

    <style>
        /* Styles personnalisés si nécessaire */
    </style>
</head>
<body class="font-sans antialiased">

    <!-- ============================================ -->
    <!-- HEADER / NAVIGATION -->
    <!-- ============================================ -->
    <header>
        <!-- Votre navigation -->
    </header>

    <!-- ============================================ -->
    <!-- MAIN CONTENT -->
    <!-- ============================================ -->
    <main>

        <!-- Section 1 -->
        <section>
        </section>

        <!-- Section 2 -->
        <section>
        </section>

        <!-- Plus de sections... -->

    </main>

    <!-- ============================================ -->
    <!-- FOOTER -->
    <!-- ============================================ -->
    <footer>
        <!-- Votre footer -->
    </footer>

</body>
</html>
```

#### Étape 3 : Suivre le design system

Référez-vous à `.context/styling/design-system.md` pour :
- **Couleurs** : Utilisez la palette définie
- **Typographie** : Suivez la hiérarchie des tailles
- **Espacements** : Utilisez l'échelle d'espacement
- **Composants** : Suivez les patterns dans `.context/components/patterns.md`

#### Étape 4 : Assurer l'accessibilité

Suivez `.context/components/accessibility.md` :

```html
<!-- ✅ Bon : Navigation accessible -->
<nav aria-label="Navigation principale">
    <ul role="list">
        <li><a href="#accueil">Accueil</a></li>
    </ul>
</nav>

<!-- ✅ Bon : Bouton avec label clair -->
<button aria-label="Ouvrir le menu" aria-expanded="false">
    <svg aria-hidden="true"><!-- icon --></svg>
</button>

<!-- ✅ Bon : Image avec alt text -->
<img src="hero.jpg" alt="Dashboard montrant les statistiques de ventes">
```

#### Étape 5 : Rendre responsive

Suivez l'approche mobile-first de `.context/styling/responsive-design.md` :

```html
<!-- Mobile d'abord, puis ajuster pour desktop -->
<div class="
    grid
    grid-cols-1      <!-- 1 colonne sur mobile -->
    md:grid-cols-2   <!-- 2 colonnes sur tablette -->
    lg:grid-cols-3   <!-- 3 colonnes sur desktop -->
    gap-6
">
    <!-- Contenu -->
</div>
```

## Structure d'un template

### Organisation des fichiers

```
nom-du-template/
├── index.html              # Fichier principal du template
├── README.md               # Documentation du template
├── preview.png             # Screenshot du template
├── components/             # Composants extraits réutilisables
│   ├── header.html
│   ├── footer.html
│   ├── card.html
│   └── ...
└── assets/                 # Assets spécifiques (optionnel)
    ├── images/
    └── data/               # Données mockées si nécessaire
```

### Contenu du README.md

Chaque template doit avoir un README avec :

```markdown
# Nom du Template

Description courte du template (1-2 phrases).

![Preview](preview.png)

## 📋 Vue d'ensemble

Description détaillée du template, cas d'usage, pour qui c'est fait.

## ✨ Fonctionnalités

- Fonctionnalité 1
- Fonctionnalité 2
- ...

## 🛠️ Technologies utilisées

- Tailwind CSS 3.x
- Alpine.js 3.x (si applicable)
- ApexCharts (si applicable)
- Autres...

## 🚀 Utilisation

### Installation rapide

```bash
# Copier vers votre projet
cp -r nom-du-template /chemin/vers/projet

# Ouvrir dans le navigateur
open index.html
```

### Intégration dans un projet existant

Instructions pour intégrer...

## 🎨 Personnalisation

### Couleurs

Instructions pour changer les couleurs...

### Contenu

Instructions pour remplacer le contenu...

### Composants

Liste des composants disponibles dans components/

## ♿ Accessibilité

- WCAG AA compliant
- Navigation au clavier
- Screen reader friendly
- ...

## 📱 Responsive

- Mobile: 320px - 767px
- Tablet: 768px - 1023px
- Desktop: 1024px+

## 📦 Composants réutilisables

### Component 1
Description et utilisation...

### Component 2
Description et utilisation...

## 🐛 Problèmes connus

Liste des limitations ou problèmes connus...

## 📄 Licence

MIT License - Utilisation libre en projet personnel et commercial.
```

### Composants extraits

Chaque composant dans `components/` doit être documenté :

```html
<!-- components/card-example.html -->

<!--
====================================
CARD COMPONENT
====================================

Description: Carte générique avec image, titre, description et CTA

Variantes disponibles :
- Default (avec image)
- Sans image
- Avec badge
- Large (pleine largeur)

Utilisation :
1. Copier le code HTML ci-dessous
2. Remplacer src, texte et href
3. Ajuster les classes Tailwind si nécessaire

Accessibilité :
- Utilise des éléments sémantiques (article, heading)
- Image avec alt text descriptif
- Lien avec aria-label clair
====================================
-->

<article class="bg-white rounded-lg shadow-md overflow-hidden hover:shadow-xl transition-shadow">
    <!-- Image -->
    <img
        src="https://via.placeholder.com/400x250"
        alt="Description de l'image"
        class="w-full h-48 object-cover"
    >

    <!-- Contenu -->
    <div class="p-6">
        <h3 class="text-xl font-bold text-gray-900 mb-2">
            Titre de la carte
        </h3>
        <p class="text-gray-600 mb-4">
            Description courte du contenu de la carte.
        </p>
        <a
            href="#"
            class="inline-block bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition-colors"
            aria-label="En savoir plus sur [sujet]"
        >
            En savoir plus
        </a>
    </div>
</article>

<!-- VARIANTE: Sans image -->
<article class="bg-white rounded-lg shadow-md p-6 hover:shadow-xl transition-shadow">
    <h3 class="text-xl font-bold text-gray-900 mb-2">
        Titre de la carte
    </h3>
    <p class="text-gray-600 mb-4">
        Description courte du contenu de la carte.
    </p>
    <a
        href="#"
        class="inline-block bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition-colors"
    >
        En savoir plus
    </a>
</article>
```

## Modifier un template existant

### Modifications simples

Pour des modifications simples (couleurs, texte, images) :

```bash
# 1. Copier le template
cp -r dashboard-modern mon-dashboard

# 2. Ouvrir index.html
cd mon-dashboard
# Éditez index.html avec votre éditeur préféré

# 3. Modifier le contenu
# - Remplacer les textes
# - Changer les images (src)
# - Ajuster les couleurs (classes Tailwind)
```

### Modifications complexes avec Claude Code

Pour des modifications structurelles :

```
"Dans dashboard-modern/index.html, modifie pour :
- Ajouter une nouvelle section 'Objectifs mensuels' après les stats
- Remplacer le graphique donut par un graphique en barres
- Ajouter un filtre par date dans le header
- Rendre la sidebar toujours visible (pas collapsible)

Maintiens la cohérence du design system .context/"
```

### Forker un template

Pour créer une variante d'un template existant :

```bash
# 1. Copier le template de base
cp -r dashboard-modern dashboard-ecommerce

# 2. Utiliser Claude Code pour adapter
```

```
"J'ai copié dashboard-modern vers dashboard-ecommerce.
Adapte ce template pour un dashboard e-commerce :

Modifications :
- Remplace les métriques financières par des métriques e-commerce
  (commandes, revenus, panier moyen, taux conversion)
- Ajoute une section 'Top Produits' avec images
- Remplace les graphiques pour montrer :
  - Ventes par jour (ligne)
  - Répartition par catégorie (donut)
  - Top 10 produits (barres)
- Ajoute des filtres par période
- Change la palette vers vert/émeraude

Maintiens la structure globale et le niveau d'accessibilité."
```

## Extraire des composants réutilisables

### Identifier les composants à extraire

Un bon candidat pour extraction est un élément qui :
- ✅ Se répète plusieurs fois
- ✅ A une structure claire et isolée
- ✅ Pourrait être réutilisé dans d'autres templates
- ✅ A des variantes possibles

**Exemples :**
- Cartes (produit, blog post, stat, etc.)
- Boutons (primary, secondary, outline, etc.)
- Formulaires (inputs, selects, checkboxes)
- Navigation (header, footer, sidebar)
- Modales et popups
- Alerts et notifications

### Processus d'extraction avec Claude Code

```
"Dans dashboard-modern/index.html, extrait la carte de statistique
(celle avec icône, label, valeur, et pourcentage de changement)
en un composant réutilisable.

Crée components/stat-card.html avec :
1. Le composant de base documenté
2. 4 variantes :
   - Success (vert, flèche montante)
   - Warning (orange, flèche latérale)
   - Danger (rouge, flèche descendante)
   - Neutral (gris, pas de flèche)
3. Instructions d'utilisation claires
4. Exemple d'intégration dans une grille
5. Props personnalisables listées
"
```

### Processus d'extraction manuel

#### Étape 1 : Identifier le code à extraire

Dans `index.html`, trouvez le composant répété :

```html
<!-- Ceci se répète plusieurs fois -->
<div class="bg-white rounded-lg shadow p-6">
    <div class="flex items-center justify-between">
        <div>
            <p class="text-sm text-gray-600">Revenus</p>
            <p class="text-2xl font-bold text-gray-900">45 231 €</p>
        </div>
        <div class="text-green-500">
            <svg><!-- icon --></svg>
        </div>
    </div>
    <p class="text-sm text-green-600 mt-2">+12.5% vs mois dernier</p>
</div>
```

#### Étape 2 : Créer le fichier du composant

Créez `components/stat-card.html` :

```html
<!--
====================================
STAT CARD COMPONENT
====================================

Description:
Carte de statistique avec label, valeur, icône et pourcentage de changement.

Props à personnaliser:
- {label}: Le label de la stat (ex: "Revenus")
- {value}: La valeur affichée (ex: "45 231 €")
- {change}: Le pourcentage de changement (ex: "+12.5%")
- {changeLabel}: Label du changement (ex: "vs mois dernier")
- {icon}: L'icône SVG
- {colorClass}: Classe de couleur (green, red, orange, gray)

Variantes:
- Success (green) - Tendance positive
- Danger (red) - Tendance négative
- Warning (orange) - Stable ou neutre
- Neutral (gray) - Sans tendance

====================================
-->

<!-- VARIANTE: Success (green) -->
<div class="bg-white rounded-lg shadow p-6">
    <div class="flex items-center justify-between">
        <div>
            <p class="text-sm text-gray-600">{label}</p>
            <p class="text-2xl font-bold text-gray-900">{value}</p>
        </div>
        <div class="text-green-500">
            <!-- Icône flèche montante -->
            <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/>
            </svg>
        </div>
    </div>
    <p class="text-sm text-green-600 mt-2">{change} {changeLabel}</p>
</div>

<!-- VARIANTE: Danger (red) -->
<div class="bg-white rounded-lg shadow p-6">
    <div class="flex items-center justify-between">
        <div>
            <p class="text-sm text-gray-600">{label}</p>
            <p class="text-2xl font-bold text-gray-900">{value}</p>
        </div>
        <div class="text-red-500">
            <!-- Icône flèche descendante -->
            <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 17h8m0 0V9m0 8l-8-8-4 4-6-6"/>
            </svg>
        </div>
    </div>
    <p class="text-sm text-red-600 mt-2">{change} {changeLabel}</p>
</div>

<!-- Plus de variantes... -->

<!--
====================================
UTILISATION
====================================

Dans votre HTML, copiez une variante et remplacez les {props} :

<div class="bg-white rounded-lg shadow p-6">
    <div class="flex items-center justify-between">
        <div>
            <p class="text-sm text-gray-600">Revenus</p>
            <p class="text-2xl font-bold text-gray-900">45 231 €</p>
        </div>
        <div class="text-green-500">
            <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/>
            </svg>
        </div>
    </div>
    <p class="text-sm text-green-600 mt-2">+12.5% vs mois dernier</p>
</div>

====================================
EXEMPLE: Grille de 4 stats
====================================

<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
    <!-- Stat 1 -->
    <div class="bg-white rounded-lg shadow p-6">
        ...
    </div>

    <!-- Stat 2 -->
    <div class="bg-white rounded-lg shadow p-6">
        ...
    </div>

    <!-- Stat 3 -->
    <div class="bg-white rounded-lg shadow p-6">
        ...
    </div>

    <!-- Stat 4 -->
    <div class="bg-white rounded-lg shadow p-6">
        ...
    </div>
</div>

====================================
-->
```

#### Étape 3 : Documenter dans le README

Ajoutez dans le README du template :

```markdown
## 📦 Composants réutilisables

### Stat Card

**Fichier:** `components/stat-card.html`

Carte de statistique avec label, valeur, icône et indicateur de tendance.

**Variantes:**
- Success (vert) - Tendance positive
- Danger (rouge) - Tendance négative
- Warning (orange) - Stable
- Neutral (gris) - Sans tendance

**Utilisation:** Voir le fichier du composant pour les exemples.
```

## Bonnes pratiques

### 1. Suivez toujours le design system

```html
<!-- ❌ Mauvais : Couleurs hardcodées -->
<div class="bg-[#3B82F6]">

<!-- ✅ Bon : Utiliser les classes Tailwind du design system -->
<div class="bg-blue-500">
```

Référez-vous à `.context/styling/design-system.md` pour les valeurs approuvées.

### 2. Commentez clairement les sections

```html
<!-- ============================================ -->
<!-- SECTION HERO -->
<!-- ============================================ -->
<section class="...">
    <!-- Contenu -->
</section>

<!-- ============================================ -->
<!-- SECTION FONCTIONNALITÉS -->
<!-- ============================================ -->
<section class="...">
    <!-- Contenu -->
</section>
```

### 3. Utilisez des noms de classes sémantiques

```html
<!-- ❌ Mauvais : Noms vagues -->
<div class="box">
<div class="thing">

<!-- ✅ Bon : Noms descriptifs -->
<article class="product-card">
<section class="features-grid">
```

### 4. Optimisez pour la performance

```html
<!-- Lazy load des images -->
<img
    src="image.jpg"
    loading="lazy"
    alt="Description"
>

<!-- Preconnect aux CDN -->
<link rel="preconnect" href="https://fonts.googleapis.com">

<!-- Defer les scripts non-critiques -->
<script defer src="script.js"></script>
```

### 5. Testez sur différents devices

Testez votre template sur :
- 📱 Mobile (320px, 375px, 414px)
- 📱 Tablet (768px, 1024px)
- 💻 Desktop (1280px, 1920px)
- 🖥️ Large screens (2560px+)

**Outils de test:**
- Chrome DevTools (F12 → Device Toolbar)
- Firefox Responsive Design Mode
- BrowserStack (pour tester sur vrais devices)

### 6. Validez l'accessibilité

**Outils:**
- **axe DevTools** (extension Chrome/Firefox)
- **WAVE** (extension Chrome)
- **Lighthouse** (Chrome DevTools)

**Tests manuels:**
- ⌨️ Navigation au clavier (Tab, Shift+Tab, Enter, Esc)
- 🎤 Screen reader (VoiceOver sur Mac, NVDA sur Windows)
- 🎨 Contraste des couleurs (ratio 4.5:1 minimum)

## Checklist de qualité

Avant de considérer un template comme terminé :

### ✅ Code

- [ ] HTML valide (pas d'erreurs dans la console)
- [ ] Classes Tailwind correctes (pas de classes inexistantes)
- [ ] Pas de styles inline (sauf dans `<script>` pour config Tailwind)
- [ ] Code indenté proprement
- [ ] Commentaires clairs sur les sections
- [ ] CDN links fonctionnels

### ✅ Design

- [ ] Suit le design system dans `.context/`
- [ ] Couleurs cohérentes
- [ ] Typographie cohérente
- [ ] Espacements cohérents
- [ ] Animations subtiles et professionnelles

### ✅ Responsive

- [ ] Fonctionne sur mobile (320px+)
- [ ] Fonctionne sur tablette (768px+)
- [ ] Fonctionne sur desktop (1024px+)
- [ ] Pas de débordement horizontal
- [ ] Images responsive

### ✅ Accessibilité

- [ ] Navigation au clavier fonctionne
- [ ] Labels ARIA présents sur éléments interactifs
- [ ] Images avec alt text
- [ ] Contraste des couleurs WCAG AA
- [ ] Structure heading logique (h1 → h2 → h3)
- [ ] Focus indicators visibles

### ✅ Performance

- [ ] Images optimisées (taille raisonnable)
- [ ] Lazy loading activé sur images
- [ ] Scripts defer ou async
- [ ] Pas de ressources bloquantes
- [ ] Temps de chargement < 3 secondes

### ✅ Documentation

- [ ] README.md complet
- [ ] Screenshot preview.png présent
- [ ] Composants documentés dans components/
- [ ] Instructions d'utilisation claires
- [ ] Liste des dépendances
- [ ] Exemples de personnalisation

### ✅ Test

- [ ] Testé dans Chrome
- [ ] Testé dans Firefox
- [ ] Testé dans Safari
- [ ] Testé sur mobile réel (si possible)
- [ ] Validé avec Lighthouse (score > 90)
- [ ] Validé avec axe DevTools (0 erreurs critiques)

## Contribuer un template

Si vous souhaitez contribuer un template à ce repository :

### 1. Préparez votre template

Assurez-vous qu'il respecte la [Checklist de qualité](#checklist-de-qualité).

### 2. Suivez la structure standard

```
votre-template/
├── index.html
├── README.md
├── preview.png
└── components/
    ├── composant1.html
    └── composant2.html
```

### 3. Créez une Pull Request

```bash
# 1. Fork le repository sur GitHub

# 2. Clone votre fork
git clone https://github.com/votre-username/.context-designs.git
cd .context-designs

# 3. Créez une branche
git checkout -b add-template-votre-nom

# 4. Ajoutez votre template
cp -r /chemin/vers/votre-template ./

# 5. Commit
git add .
git commit -m "Add new template: Votre Template"

# 6. Push
git push origin add-template-votre-nom

# 7. Créez une Pull Request sur GitHub
```

### 4. Description de la Pull Request

Dans la PR, incluez :

```markdown
## Nouveau Template: [Nom]

### Description
[Description courte du template]

### Type
- [ ] Landing page
- [ ] Dashboard
- [ ] Blog
- [ ] E-commerce
- [ ] Autre: _______

### Checklist
- [ ] README.md complet
- [ ] Screenshot preview.png
- [ ] Responsive testé
- [ ] Accessibilité validée (WCAG AA)
- [ ] Suit le design system .context/
- [ ] Composants extraits et documentés
- [ ] Testé dans Chrome, Firefox, Safari

### Screenshots
[Ajoutez des screenshots]

### Démo live (optionnel)
[Lien vers une démo live si disponible]
```

## Ressources

### Templates de référence

Étudiez ces templates pour comprendre les patterns :
- `dashboard-modern/` - Exemple complet de dashboard
- `landing-page-fintech/` - Exemple de landing page
- `dashboard-leads/` - Variation de dashboard

### Documentation .context

- `.context/substrate.md` - Vue d'ensemble
- `.context/styling/design-system.md` - Design system
- `.context/components/patterns.md` - Patterns de composants
- `.context/templates/creation-guide.md` - Guide de création détaillé

### Outils utiles

- **Tailwind CSS Docs:** https://tailwindcss.com/docs
- **Alpine.js Docs:** https://alpinejs.dev/
- **ApexCharts Docs:** https://apexcharts.com/
- **Heroicons:** https://heroicons.com/
- **Can I Use:** https://caniuse.com/ (compatibilité navigateurs)
- **WebAIM Contrast Checker:** https://webaim.org/resources/contrastchecker/

---

**Prêt à créer votre premier template ?** 🚀

Retour au [Guide de démarrage rapide](QUICKSTART.md) | Voir le [Guide Claude Code](CLAUDE-CODE-GUIDE.md)
