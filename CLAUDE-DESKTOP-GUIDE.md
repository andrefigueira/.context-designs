# Guide d'utilisation avec Claude Desktop

Ce guide vous explique comment utiliser **Claude Desktop** (l'application de bureau d'Anthropic) avec ce projet pour un workflow de développement fluide.

## 📋 Table des matières

- [Claude Desktop vs Claude Code](#claude-desktop-vs-claude-code)
- [Installation](#installation)
- [Configuration pour ce projet](#configuration-pour-ce-projet)
- [Workflows avec Claude Desktop](#workflows-avec-claude-desktop)
- [Intégration avec votre éditeur](#intégration-avec-votre-éditeur)
- [Bonnes pratiques](#bonnes-pratiques)
- [Cas d'usage](#cas-dusage)

## Claude Desktop vs Claude Code

### Quelle est la différence ?

**Claude Code** (CLI)
- Outil en ligne de commande
- Accès direct aux fichiers du projet
- Peut lire, écrire, et modifier des fichiers
- Idéal pour le développement actif

**Claude Desktop** (Application)
- Application graphique de bureau
- Interface conversationnelle
- Peut analyser des fichiers uploadés
- Idéal pour la consultation, la planification, et les revues de code

### Quand utiliser quoi ?

| Tâche | Claude Code | Claude Desktop |
|-------|-------------|----------------|
| Générer du code | ✅ Recommandé | ⚠️ Copier-coller nécessaire |
| Modifier des fichiers | ✅ Direct | ❌ Manuel |
| Analyser du code | ✅ | ✅ |
| Planifier une feature | ✅ | ✅ Excellent |
| Review de code | ✅ | ✅ Excellent |
| Expliquer un concept | ✅ | ✅ |
| Brainstorming de design | ⚠️ | ✅ Excellent |
| Créer des mockups | ❌ | ✅ (avec description) |

**💡 Workflow optimal :** Utilisez Claude Desktop pour planifier, puis Claude Code pour implémenter.

## Installation

### Prérequis

- **Système d'exploitation :** macOS, Windows, ou Linux
- **Compte Claude** : Gratuit ou Pro

### Téléchargement et installation

1. **Visitez le site officiel**
   - https://claude.ai/download

2. **Téléchargez pour votre OS**
   - macOS : .dmg
   - Windows : .exe
   - Linux : .AppImage ou .deb

3. **Installez l'application**
   - **macOS** : Glissez Claude.app vers Applications
   - **Windows** : Exécutez le .exe et suivez l'installateur
   - **Linux** :
     ```bash
     # Pour .deb
     sudo dpkg -i claude-desktop.deb

     # Pour .AppImage
     chmod +x Claude-Desktop.AppImage
     ./Claude-Desktop.AppImage
     ```

4. **Lancez Claude Desktop**
   - Connectez-vous avec votre compte Claude

## Configuration pour ce projet

### Méthode 1 : Upload de fichiers (Simple)

Claude Desktop ne peut pas accéder directement à votre système de fichiers, mais vous pouvez uploader des fichiers pour analyse.

**Workflow :**

1. Ouvrez Claude Desktop
2. Cliquez sur l'icône 📎 (trombone) pour attacher un fichier
3. Sélectionnez les fichiers pertinents de votre projet

**Fichiers à uploader pour contexte complet :**

```
.context-designs/
├── .context/
│   ├── substrate.md              ← Vue d'ensemble
│   ├── styling/design-system.md  ← Design system
│   └── components/patterns.md    ← Patterns
├── README.md                      ← Documentation principale
└── dashboard-modern/index.html    ← Exemple de template
```

**Taille des fichiers :** Claude Desktop accepte plusieurs fichiers simultanément.

### Méthode 2 : Copier-coller (Rapide pour petits extraits)

Pour des questions rapides, copiez-collez le code directement :

```
Voici le code de mon composant :

```html
[Coller votre code HTML ici]
```

Question : Comment puis-je améliorer l'accessibilité de ce composant ?
```

### Méthode 3 : Contexte via conversation

Décrivez votre projet en texte :

```
Je travaille sur le projet .context-designs qui contient des templates
Tailwind CSS. Le design system utilise :
- Couleur primaire : blue-500
- Espacement standard : p-6, gap-6
- Bordures : rounded-lg
- Ombres : shadow-md

J'ai besoin d'aide pour créer un nouveau composant de carte produit.
```

## Workflows avec Claude Desktop

### Workflow 1 : Planification de feature

**Utilisation optimale de Claude Desktop**

```
📝 Dans Claude Desktop :

"Je veux ajouter un template de blog à .context-designs.

Contexte du projet :
- Repository de templates Tailwind CSS
- Design system documenté dans .context/
- Templates existants : dashboard-modern, landing-page-fintech

Besoin :
- Template de blog moderne
- Grille de posts
- Filtrage par catégorie
- Sidebar avec posts populaires
- Accessible WCAG AA

Question : Peux-tu me créer un plan détaillé pour implémenter ce template ?
Inclus :
1. Structure des sections
2. Composants à créer
3. Fonctionnalités interactives
4. Ordre d'implémentation recommandé
"
```

**Claude Desktop vous donnera :**
- ✅ Plan structuré et détaillé
- ✅ Liste de composants nécessaires
- ✅ Suggestions d'architecture
- ✅ Ordre d'implémentation optimal

**Ensuite, utilisez Claude Code pour implémenter ce plan.**

### Workflow 2 : Review de code

**Upload du fichier dans Claude Desktop :**

1. Uploadez `dashboard-modern/index.html`
2. Demandez une review :

```
"Peux-tu analyser ce template et identifier :
1. Points forts
2. Problèmes potentiels
3. Améliorations d'accessibilité possibles
4. Optimisations de performance
5. Cohérence avec les best practices Tailwind

Sois spécifique avec des exemples de code."
```

**Claude Desktop excellera pour :**
- ✅ Analyse approfondie
- ✅ Suggestions détaillées
- ✅ Explications pédagogiques

### Workflow 3 : Brainstorming de design

```
"Je veux créer un dashboard pour une application de gestion de projets.

Inspiration :
- Linear (minimaliste)
- Notion (organisé)
- Asana (coloré)

Contraintes :
- Tailwind CSS uniquement
- Design system : bleu/gris
- Accessible
- Responsive

Peux-tu me proposer :
1. 3 variations de layout
2. Sections principales à inclure
3. Patterns de navigation
4. Idées pour les visualisations de données

Décris chaque variation en détail."
```

**Avantage de Claude Desktop :**
- ✅ Réponses longues et détaillées
- ✅ Multiple options explorées
- ✅ Raisonnement expliqué

### Workflow 4 : Debugging et explication

**Uploadez le fichier problématique :**

```
"Ce composant ne fonctionne pas correctement sur mobile.
[Upload du fichier]

Problème observé :
- La sidebar ne se ferme pas sur mobile
- Le bouton hamburger ne répond pas

Peux-tu :
1. Identifier le problème
2. Expliquer pourquoi ça ne fonctionne pas
3. Proposer une solution
4. Me donner le code corrigé
"
```

### Workflow 5 : Apprendre et comprendre

**Excellente utilisation de Claude Desktop :**

```
"J'ai téléchargé dashboard-modern/index.html.
[Upload du fichier]

Je suis débutant en Tailwind CSS. Peux-tu :
1. M'expliquer la structure du layout
2. Détailler comment fonctionne la grille responsive
3. Expliquer les classes Tailwind utilisées section par section
4. Me montrer comment je pourrais modifier les couleurs

Explique comme si j'étais débutant."
```

## Intégration avec votre éditeur

### VS Code + Claude Desktop

**Workflow efficace :**

1. **VS Code :** Ouvrez votre projet
2. **Claude Desktop :** Gardez l'app ouverte à côté
3. **Workflow :**
   - Posez vos questions dans Claude Desktop
   - Obtenez le code généré
   - Copiez dans VS Code
   - Testez et itérez

**Astuce :** Utilisez un second moniteur pour Claude Desktop.

### Cursor + Claude Desktop

Si vous utilisez Cursor (éditeur AI-powered) :

1. **Cursor :** Pour les modifications rapides en ligne
2. **Claude Desktop :** Pour la planification et l'architecture
3. **Complémentarité :**
   - Claude Desktop = Réflexion
   - Cursor = Exécution

## Bonnes pratiques

### 1. Fournissez du contexte clair

**❌ Mauvais :**
```
"Comment faire une carte ?"
```

**✅ Bon :**
```
"Je travaille sur .context-designs, un projet de templates Tailwind CSS.
[Upload de .context/styling/design-system.md]

J'ai besoin de créer une carte produit qui suit ce design system.
La carte doit avoir : image, titre, prix, description, bouton CTA.

Peux-tu me générer le code HTML avec Tailwind en suivant
le design system uploadé ?"
```

### 2. Uploadez les fichiers pertinents

Pour une meilleure compréhension :

**Fichiers essentiels à uploader :**
- `.context/substrate.md` → Contexte général
- `.context/styling/design-system.md` → Design system
- Le fichier que vous voulez modifier/analyser

### 3. Posez des questions spécifiques

**❌ Vague :**
```
"C'est quoi ce code ?"
```

**✅ Spécifique :**
```
"Dans ce fichier [upload], comment fonctionne l'interactivité de la sidebar ?
Plus précisément, explique-moi le rôle de Alpine.js et les attributs x-data, x-show."
```

### 4. Itérez progressivement

Au lieu d'une grosse demande :

```
1. "Crée la structure de base du composant"
   → Validez

2. "Ajoute l'interactivité"
   → Validez

3. "Améliore l'accessibilité"
   → Validez

4. "Ajoute des animations"
   → Validez
```

### 5. Utilisez pour la documentation

Claude Desktop excelle pour :

```
"J'ai créé ce template [upload].
Peux-tu me générer un README.md complet avec :
- Description
- Fonctionnalités
- Instructions d'installation
- Guide de personnalisation
- Liste des composants
?"
```

## Cas d'usage

### Cas 1 : Vous débutez avec ce projet

**Session avec Claude Desktop :**

```
1. Uploadez README.md

2. "Peux-tu m'expliquer ce projet en termes simples ?
   - À quoi ça sert ?
   - Comment je peux l'utiliser ?
   - Par où commencer ?"

3. Uploadez un template (ex: dashboard-modern/index.html)

4. "Peux-tu me faire un tour guidé de ce template ?
   Explique chaque section et comment elle fonctionne."
```

### Cas 2 : Vous voulez créer un nouveau template

**Phase 1 - Planification (Claude Desktop) :**

```
"Je veux créer un template de portfolio pour développeur.

Sections souhaitées :
- Hero avec photo et intro
- Liste de projets (grille)
- Compétences (badges)
- Contact

Contraintes :
- Tailwind CSS
- Accessible
- Animé au scroll
- Dark mode

Peux-tu me créer un plan détaillé d'implémentation ?"
```

**Phase 2 - Implémentation (Claude Code) :**

```bash
# Utilisez Claude Code dans le terminal pour générer le code
claude-code "Crée le template portfolio selon le plan..."
```

### Cas 3 : Vous avez un bug

**Dans Claude Desktop :**

```
1. Upload du fichier problématique

2. "J'ai un problème avec ce template [upload] :
   - Description du bug
   - Comportement attendu
   - Comportement actuel
   - Navigateur et device

   Peux-tu identifier le problème et proposer une solution ?"
```

### Cas 4 : Vous voulez améliorer un template existant

**Dans Claude Desktop :**

```
1. Upload du template actuel

2. "Analyse ce template et suggère 10 améliorations :
   - Performance
   - Accessibilité
   - Design
   - Code quality
   - UX

   Priorise par impact."
```

### Cas 5 : Apprendre les best practices

**Dans Claude Desktop :**

```
1. Upload d'un template exemple (ex: dashboard-modern)

2. "Ce template représente les best practices.
   Peux-tu extraire et m'expliquer :

   - Patterns Tailwind CSS utilisés
   - Structure HTML sémantique
   - Techniques d'accessibilité
   - Approche responsive
   - Organisation du code

   Pour chaque point, donne-moi des exemples concrets du code."
```

## Fonctionnalités avancées

### Analyse d'images

Claude Desktop peut analyser des screenshots :

```
1. Prenez un screenshot de votre design
2. Uploadez dans Claude Desktop
3. "Voici un mockup de design [upload screenshot].
   Peux-tu me générer le code HTML + Tailwind pour recréer ce design ?"
```

### Génération de variantes

```
Upload dashboard-modern/index.html

"Crée 3 variantes de ce dashboard :
1. Version dark mode
2. Version avec sidebar droite
3. Version sans sidebar (top navigation)

Pour chaque variante, décris les changements principaux
et donne-moi le code modifié pour les sections clés."
```

### Documentation automatique

```
Upload de plusieurs composants

"J'ai ces 5 composants [uploads].
Génère une documentation Markdown qui :
- Décrit chaque composant
- Liste les props/variants
- Donne des exemples d'utilisation
- Explique quand utiliser chaque composant
"
```

## Limites et solutions

### ❌ Limite : Pas d'accès direct aux fichiers

**Solution :**
- Upload manuel des fichiers nécessaires
- Ou utilisez Claude Code pour accès direct

### ❌ Limite : Copier-coller nécessaire pour le code généré

**Solution :**
- Utilisez Claude Code pour génération directe dans les fichiers
- Ou copiez le code de Claude Desktop → VS Code

### ❌ Limite : Taille limite d'upload

**Solution :**
- Uploadez seulement les fichiers pertinents
- Résumez le contexte en texte si nécessaire

### ❌ Limite : Pas de preview live

**Solution :**
- Testez le code généré dans votre navigateur
- Utilisez un serveur local pour voir les changements en temps réel

## Comparaison des workflows

### Workflow "Claude Desktop seul"

```
1. Planification dans Claude Desktop
2. Génération de code dans Claude Desktop
3. Copier-coller dans votre éditeur
4. Test dans navigateur
5. Retour à Claude Desktop pour ajustements
6. Répéter 2-5
```

**⚠️ Plus lent mais fonctionne**

### Workflow "Claude Code seul"

```
1. Prompt dans Claude Code
2. Code généré directement dans les fichiers
3. Test dans navigateur
4. Ajustements dans Claude Code
5. Répéter 3-4
```

**✅ Plus rapide pour l'implémentation**

### Workflow "Hybride" (Recommandé)

```
1. Planification et architecture dans Claude Desktop
2. Implémentation avec Claude Code
3. Review et optimisation dans Claude Desktop
4. Corrections finales avec Claude Code
```

**✅✅ Le meilleur des deux mondes**

## Ressources

### Documentation officielle

- **Claude Desktop :** https://www.anthropic.com/claude
- **Support Claude :** https://support.anthropic.com/

### Guides connexes

- [Guide de démarrage rapide](QUICKSTART.md)
- [Guide Claude Code](CLAUDE-CODE-GUIDE.md)
- [Guide des templates](TEMPLATE-GUIDE.md)

---

**Claude Desktop est parfait pour la réflexion et la planification.** 💡
**Claude Code est parfait pour l'implémentation rapide.** ⚡

**Utilisez les deux pour un workflow optimal !** 🚀

Retour au [Guide de démarrage rapide](QUICKSTART.md)
