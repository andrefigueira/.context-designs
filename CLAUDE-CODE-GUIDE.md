# Guide d'utilisation avec Claude Code

Ce guide vous explique comment utiliser **Claude Code** avec ce projet pour générer des composants et templates UI de manière cohérente et rapide.

## 📋 Table des matières

- [Qu'est-ce que Claude Code ?](#quest-ce-que-claude-code-)
- [Installation](#installation)
- [Configuration initiale](#configuration-initiale)
- [Utilisation basique](#utilisation-basique)
- [Workflows avancés](#workflows-avancés)
- [Prompts efficaces](#prompts-efficaces)
- [Comprendre la méthodologie .context](#comprendre-la-méthodologie-context)
- [Résolution de problèmes](#résolution-de-problèmes)

## Qu'est-ce que Claude Code ?

**Claude Code** est l'outil CLI officiel d'Anthropic pour le développement assisté par IA. Il comprend les workflows de développement logiciel et peut lire, éditer, et créer du code.

### Pourquoi Claude Code + .context = Puissance

**Le problème avec l'IA générique :**
```
Vous : "Crée un dashboard"
IA : [Génère du code avec des couleurs aléatoires]
Vous : "Non, utilise du bleu"
IA : [Change en bleu générique]
Vous : "Non, mon bleu à moi : #3B82F6"
IA : [Ajuste mais ne se souvient pas]
Vous : "Crée un autre composant dans le même style"
IA : [Recommence de zéro, couleurs différentes]
```

**Avec Claude Code + .context :**
```
Vous : (Une fois) Documentez vos standards dans .context/
      - Couleurs : primary-blue = #3B82F6
      - Espacements : card-padding = p-6
      - Accessibilité : Toujours WCAG AA

Vous : "Crée un dashboard"
Claude Code : [Lit .context/, génère avec #3B82F6, p-6, WCAG AA]

Vous : "Crée une page de pricing"
Claude Code : [Automatiquement cohérent, mêmes standards]

Vous : "Crée un blog layout"
Claude Code : [Toujours cohérent, zéro répétition nécessaire]
```

## Installation

### Prérequis

- **Système d'exploitation :** macOS, Linux, ou Windows (WSL2)
- **Compte Anthropic :** Nécessaire pour utiliser Claude Code
- **Accès API Claude** (ou abonnement Claude Pro)

### Étapes d'installation

#### 1. Installer Claude Code

**macOS / Linux :**
```bash
# Via le script d'installation officiel
curl -fsSL https://claude.com/install.sh | sh
```

**Windows (WSL2) :**
```bash
# Installer dans WSL2
curl -fsSL https://claude.com/install.sh | sh
```

**Alternative - Installation manuelle :**
Visitez : https://docs.claude.com/en/docs/claude-code

#### 2. Vérifier l'installation

```bash
# Vérifier que Claude Code est installé
claude-code --version

# Devrait afficher quelque chose comme : claude-code v1.x.x
```

#### 3. Authentification

```bash
# Se connecter à votre compte Anthropic
claude-code login

# Suivez les instructions pour vous authentifier
```

## Configuration initiale

### 1. Cloner ce repository

```bash
git clone https://github.com/Mediatros/.context-designs.git
cd .context-designs
```

### 2. Comprendre la structure

```
.context-designs/
├── .context/              ← Claude Code lit automatiquement ce dossier
│   ├── substrate.md      ← Vue d'ensemble du projet
│   ├── styling/
│   │   ├── design-system.md    ← Votre système de design
│   │   ├── conventions.md      ← Conventions Tailwind
│   │   └── ...
│   ├── components/
│   │   ├── patterns.md         ← Patterns de composants
│   │   ├── accessibility.md    ← Standards d'accessibilité
│   │   └── ...
│   └── ...
│
├── dashboard-modern/      ← Templates existants
├── landing-page-fintech/
└── ...
```

### 3. Lancer Claude Code

```bash
# Dans le dossier du repository
cd .context-designs

# Lancer Claude Code
claude-code

# Ou lancer avec un prompt initial
claude-code "Explique-moi la structure de ce projet"
```

## Utilisation basique

### Scénario 1 : Créer un nouveau composant

**Prompt simple :**
```
Crée une carte de produit avec :
- Image responsive
- Titre
- Description (2 lignes max)
- Prix avec badge promo
- Bouton "Ajouter au panier"

Suis le design system dans .context/ et assure-toi que c'est accessible.
```

**Ce que Claude Code fait automatiquement :**
1. ✅ Lit `.context/styling/design-system.md` pour les couleurs et espacements
2. ✅ Lit `.context/components/patterns.md` pour la structure
3. ✅ Lit `.context/components/accessibility.md` pour l'accessibilité
4. ✅ Génère du code HTML + Tailwind cohérent
5. ✅ Ajoute les attributs ARIA appropriés
6. ✅ Crée un design responsive mobile-first

**Résultat :** Code prêt à copier-coller.

### Scénario 2 : Modifier un template existant

**Prompt :**
```
Prends le dashboard-modern/index.html et modifie-le pour :
- Changer le thème de couleur vers du vert (emerald)
- Ajouter une nouvelle carte "Taux de conversion"
- Rendre la sidebar plus étroite

Maintiens la cohérence du design system.
```

**Claude Code :**
1. Lit le fichier `dashboard-modern/index.html`
2. Comprend la structure existante
3. Applique les modifications demandées
4. Maintient la cohérence avec `.context/`

### Scénario 3 : Extraire un composant réutilisable

**Prompt :**
```
Dans dashboard-modern/index.html, extrait la carte de statistique
(celle avec l'icône, le titre, la valeur, et le pourcentage de changement)
en un composant réutilisable.

Crée le fichier components/stat-card.html avec :
- Le composant documenté
- Des variantes (success, warning, danger)
- Instructions d'utilisation
```

**Claude Code crée :**
- `components/stat-card.html` avec le composant
- Documentation claire des props/variantes
- Exemples d'utilisation

## Workflows avancés

### Workflow 1 : Créer un template complet de A à Z

**Étape par étape avec Claude Code :**

```
1. "Crée un template de page de pricing avec 3 tiers (Basic, Pro, Enterprise).
   Structure :
   - Header avec navigation
   - Section hero avec titre et sous-titre
   - Grille de 3 cartes de pricing
   - Toggle mensuel/annuel
   - Tableau de comparaison des fonctionnalités
   - FAQ accordéon
   - Footer avec liens

   Suis le design system .context/ et assure WCAG AA."

2. Claude Code génère le fichier complet

3. "Extrait les composants réutilisables :
   - PricingCard
   - FeatureComparisonTable
   - FAQAccordion"

4. Claude Code crée les fichiers de composants

5. "Crée un README.md pour ce template avec :
   - Aperçu et screenshot
   - Instructions d'installation
   - Guide de personnalisation
   - Structure des composants"

6. "Ajoute un screenshot de preview"
```

**Résultat :** Template complet et documenté en 10-15 minutes.

### Workflow 2 : Adapter un template pour un nouveau contexte

**Prompt :**
```
Prends le landing-page-fintech comme base et adapte-le pour une application SaaS B2B.

Modifications :
- Remplace les mockups de téléphone par des screenshots desktop
- Adapte le vocabulaire (fintech → SaaS)
- Ajoute une section de témoignages clients entreprise
- Ajoute une section d'intégrations avec logos partenaires
- Change la palette vers bleu/gris corporate

Maintiens la structure et les patterns de .context/
```

### Workflow 3 : Améliorer l'accessibilité d'un template

**Prompt :**
```
Analyse dashboard-modern/index.html pour l'accessibilité.

Vérifie et améliore :
- Navigation au clavier
- Labels ARIA manquants
- Contraste des couleurs (WCAG AA)
- Focus indicators
- Structure heading (h1, h2, h3)
- Alt text sur les images
- Roles ARIA sur les éléments interactifs

Applique les corrections et documente les changements.
```

### Workflow 4 : Générer des variantes de composants

**Prompt :**
```
À partir du bouton principal défini dans .context/components/patterns.md,
génère 6 variantes :

1. Button Primary (défaut)
2. Button Secondary
3. Button Outline
4. Button Ghost
5. Button Destructive
6. Button avec Icon

Pour chaque variante :
- Code HTML + Tailwind
- État disabled
- État loading
- Responsive
- Accessible

Crée components/buttons.html avec toutes les variantes et exemples.
```

## Prompts efficaces

### Structure d'un bon prompt

```
[ACTION] + [DÉTAILS] + [CONTRAINTES] + [CONTEXTE .context/]

Exemple :
"Crée [ACTION] une navigation responsive [DÉTAILS] avec logo, menu principal,
bouton CTA et menu utilisateur [DÉTAILS SUPPLÉMENTAIRES]. Assure-toi que c'est
accessible au clavier et suit notre design system [CONTRAINTES].
Utilise les conventions dans .context/ [CONTEXTE]."
```

### Exemples de prompts efficaces

#### ✅ Bon prompt (spécifique + référence .context)

```
"Crée un composant de carte blog avec image 16:9, catégorie badge,
titre, excerpt (3 lignes), auteur avec avatar, date, et temps de lecture.
Suis le design system dans .context/styling/design-system.md et
rends-le accessible selon .context/components/accessibility.md."
```

#### ❌ Prompt vague (trop générique)

```
"Fais-moi une carte de blog"
```

#### ✅ Bon prompt (modification contextuelle)

```
"Dans dashboard-modern/index.html, remplace le graphique en donut
par un graphique en barres horizontales montrant les top 5 produits vendus.
Garde le style ApexCharts existant et la palette de couleurs du design system."
```

#### ❌ Prompt incomplet

```
"Change le graphique"
```

### Prompts par cas d'usage

#### Créer un composant

```
"Crée un [TYPE] avec [ÉLÉMENTS]. Suis .context/ et rends-le [CONTRAINTES]."
```

#### Modifier un fichier

```
"Dans [FICHIER], [ACTION] pour [OBJECTIF]. Maintiens [CONTRAINTES]."
```

#### Extraire un composant

```
"Extrait [ÉLÉMENT] de [FICHIER] en composant réutilisable dans [DESTINATION].
Documente les variantes et l'utilisation."
```

#### Débugger / Améliorer

```
"Analyse [FICHIER] pour [ASPECT]. Identifie les problèmes et applique les corrections
selon les standards dans .context/"
```

## Comprendre la méthodologie .context

### Pourquoi .context existe

La documentation traditionnelle devient obsolète dès qu'elle est écrite. Avec .context :

1. **Documentation = Source de vérité**
   - Vous documentez vos standards une fois
   - Claude Code les lit automatiquement
   - Génération cohérente à chaque fois

2. **Documentation vivante**
   - La doc évolue avec le code
   - Toujours synchronisée
   - Claude Code s'adapte automatiquement

### Structure .context expliquée

```
.context/
├── substrate.md              # 🎯 Vue d'ensemble du projet
│                             # Philosophie, objectifs, stack technique
│
├── architecture/             # 🏗️ Organisation du code
│   ├── overview.md          # Structure des dossiers et fichiers
│   ├── dependencies.md      # Dépendances et outils
│   └── patterns.md          # Patterns architecturaux
│
├── components/               # 🧩 Standards des composants
│   ├── patterns.md          # Comment structurer un composant
│   ├── accessibility.md     # Standards WCAG et ARIA
│   ├── interactivity.md     # JavaScript et Alpine.js
│   └── state-management.md  # Gestion d'état
│
├── styling/                  # 🎨 Design system
│   ├── design-system.md     # Couleurs, typo, espacements
│   ├── conventions.md       # Comment utiliser Tailwind
│   ├── responsive-design.md # Stratégies responsive
│   └── theming.md           # Thèmes et dark mode
│
└── templates/                # 📄 Guide des templates
    ├── creation-guide.md    # Comment créer un template
    └── maintenance.md       # Comment maintenir un template
```

### Comment Claude Code utilise .context

1. **Vous donnez un prompt**
2. **Claude Code lit automatiquement les fichiers .context/ pertinents**
3. **Claude Code génère du code qui suit vos standards documentés**
4. **Résultat cohérent avec votre design system**

### Personnaliser .context pour votre projet

Vous pouvez copier cette structure et l'adapter :

```bash
# Copier .context vers votre projet
cp -r .context /chemin/vers/votre-projet/

# Personnaliser les fichiers
cd /chemin/vers/votre-projet/.context
# Éditez styling/design-system.md avec VOS couleurs
# Éditez components/patterns.md avec VOS patterns
# etc.
```

**Maintenant Claude Code générera du code suivant VOS standards !**

## Commandes et fonctionnalités

### Commandes utiles dans Claude Code

```bash
# Lire un fichier
"Lis dashboard-modern/index.html"

# Chercher dans le code
"Trouve tous les composants qui utilisent Alpine.js"

# Expliquer du code
"Explique comment fonctionne l'interactivité de la sidebar dans dashboard-modern"

# Comparer des fichiers
"Quelles sont les différences entre dashboard-modern et dashboard-leads ?"

# Générer de la documentation
"Crée un README.md pour le dossier components/ expliquant chaque composant"

# Optimiser
"Analyse dashboard-modern/index.html et suggère des optimisations de performance"
```

### Fonctionnalités avancées

#### Itération rapide

```
Vous : "Crée une carte produit"
Claude Code : [Génère le code]

Vous : "Ajoute un badge 'Nouveau' en haut à droite"
Claude Code : [Modifie le code précédent]

Vous : "Rends le prix plus gros et en gras"
Claude Code : [Ajuste]

Vous : "Parfait ! Sauvegarde ça dans components/product-card.html"
Claude Code : [Crée le fichier]
```

#### Génération batch

```
"Crée 5 variantes de cette carte produit :
1. Standard
2. En promotion (avec badge rouge)
3. Épuisé (grisé, bouton disabled)
4. Recommandé (badge étoile)
5. Nouveau (badge vert)

Crée un fichier HTML avec les 5 variantes côte à côte pour comparaison."
```

## Résolution de problèmes

### Problème : Claude Code ne suit pas mon design system

**Solution :**
1. Vérifiez que `.context/styling/design-system.md` est bien rempli
2. Soyez explicite dans votre prompt : "Suis le design system dans .context/"
3. Référencez le fichier spécifique : "Utilise les couleurs définies dans .context/styling/design-system.md"

### Problème : Le code généré n'est pas accessible

**Solution :**
1. Vérifiez `.context/components/accessibility.md`
2. Prompt : "Crée [composant] en suivant WCAG AA selon .context/components/accessibility.md"
3. Ou : "Améliore l'accessibilité de [fichier] selon nos standards .context/"

### Problème : Incohérence entre plusieurs composants générés

**Solution :**
1. Assurez-vous que `.context/` est bien documenté
2. Générez tous les composants dans la même session Claude Code
3. Ou : "Assure-toi que ce composant est cohérent avec [autre-composant.html]"

### Problème : Claude Code ne trouve pas les fichiers

**Solution :**
```bash
# Vérifier que vous êtes dans le bon dossier
pwd
# Devrait afficher : /chemin/.context-designs

# Lister les fichiers
ls -la

# Si .context n'existe pas, vous n'êtes pas au bon endroit
```

### Problème : Tailwind CSS ne fonctionne pas

**Solution :**
1. Vérifiez que le CDN Tailwind est bien dans le `<head>` :
```html
<script src="https://cdn.tailwindcss.com"></script>
```

2. Pour la production, installez Tailwind :
```bash
npm install -D tailwindcss
npx tailwindcss init
```

## Bonnes pratiques

### 1. Documentez avant de générer

```
❌ Mauvais workflow :
   Prompt → Ajuster → Prompt → Ajuster → Répéter ∞

✅ Bon workflow :
   Documenter .context/ → Prompt simple → Code parfait du premier coup
```

### 2. Soyez spécifique dans vos prompts

```
❌ "Crée un formulaire"
✅ "Crée un formulaire de contact avec nom, email, sujet, message,
   checkbox RGPD et bouton submit. Validation inline, accessible,
   suit le design system .context/"
```

### 3. Utilisez les templates existants comme référence

```
"Crée une page similaire à landing-page-fintech mais pour une app mobile"
"Utilise le même pattern de cartes que dans dashboard-modern"
```

### 4. Itérez par petites étapes

```
1. "Crée la structure de base"
2. "Ajoute l'interactivité"
3. "Améliore l'accessibilité"
4. "Ajoute les animations"
```

### 5. Testez au fur et à mesure

```
"Crée le composant"
→ Testez dans le navigateur
"Ajuste la couleur du bouton"
→ Testez à nouveau
"Parfait ! Documente ce composant"
```

## Exemples complets

### Exemple 1 : Créer une page "À propos" complète

**Session complète avec Claude Code :**

```
🔵 Prompt 1 :
"Crée une page À propos (about.html) avec :
- Header avec navigation (même que landing-page-fintech)
- Hero section avec titre, sous-titre et image d'équipe
- Section Mission avec texte et valeurs (3 colonnes)
- Section Équipe (grille 3x2 avec photos, noms, rôles)
- Section Timeline de l'entreprise
- CTA section pour nous rejoindre
- Footer (même que landing-page-fintech)

Suis le design system .context/ et assure WCAG AA."

⚙️ Claude Code génère about.html

🔵 Prompt 2 :
"Ajoute des animations d'apparition au scroll pour les sections.
Utilise Alpine.js comme dans les autres templates."

⚙️ Claude Code ajoute l'interactivité

🔵 Prompt 3 :
"Extrait la carte de membre d'équipe en composant réutilisable
dans components/team-member-card.html avec documentation."

⚙️ Claude Code crée le composant

🔵 Prompt 4 :
"Crée un README.md pour about.html expliquant la structure,
les composants utilisés, et comment personnaliser."

⚙️ Claude Code crée la documentation

✅ Résultat : Page complète, interactive, documentée en 15 minutes !
```

### Exemple 2 : Créer un système de composants UI

```
🔵 Session Claude Code :

1. "Crée components/ui-kit/ et génère ces composants selon .context/ :
   - buttons.html (6 variantes)
   - cards.html (4 variantes)
   - forms.html (inputs, textarea, select, checkbox, radio)
   - modals.html (3 tailles)
   - alerts.html (success, warning, error, info)
   - badges.html (5 couleurs)
   - tooltips.html

   Chaque fichier doit inclure :
   - Tous les états (normal, hover, focus, disabled)
   - Exemples d'utilisation
   - Code copy-pastable
   - Documentation des variantes"

2. "Crée ui-kit/index.html qui affiche tous les composants
   organisés par catégorie avec navigation"

3. "Crée ui-kit/README.md documentant l'utilisation de chaque composant"

✅ Résultat : Bibliothèque de composants complète !
```

## Ressources

### Documentation officielle

- **Claude Code Docs :** https://docs.claude.com/en/docs/claude-code
- **Méthodologie .context :** https://github.com/andrefigueira/.context/
- **Tailwind CSS :** https://tailwindcss.com/docs
- **Alpine.js :** https://alpinejs.dev/

### Liens utiles

- **ApexCharts :** https://apexcharts.com/
- **Heroicons :** https://heroicons.com/
- **WCAG Guidelines :** https://www.w3.org/WAI/WCAG21/quickref/

---

**Prêt à créer avec Claude Code ?** 🚀

Retour au [Guide de démarrage rapide](QUICKSTART.md) | Voir le [Guide des templates](TEMPLATE-GUIDE.md)
