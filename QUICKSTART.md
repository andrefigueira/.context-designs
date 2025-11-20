# Guide de Démarrage Rapide

Bienvenue sur **.context-designs** ! Ce guide vous permettra de démarrer en moins de 5 minutes.

## 📋 Table des matières

- [Qu'est-ce que c'est ?](#quest-ce-que-cest-)
- [Démarrage en 3 étapes](#démarrage-en-3-étapes)
- [Utiliser un template existant](#utiliser-un-template-existant)
- [Créer avec Claude Code](#créer-avec-claude-code)
- [Guides détaillés](#guides-détaillés)

## Qu'est-ce que c'est ?

Une collection de **templates UI modernes** construits avec Tailwind CSS, générés par **Claude Code** en suivant la **méthodologie .context**.

**Résultat :** Du code production-ready, accessible (WCAG AA), responsive, et cohérent.

## Démarrage en 3 étapes

### 1️⃣ Cloner le repository

```bash
git clone https://github.com/Mediatros/.context-designs.git
cd .context-designs
```

### 2️⃣ Explorer les templates

```bash
# Voir tous les templates disponibles
ls -d */

# Templates actuels :
# - dashboard-modern/      → Dashboard analytique moderne
# - landing-page-fintech/  → Landing page pour fintech
# - dashboard-leads/       → Dashboard de gestion de leads
```

### 3️⃣ Tester un template

```bash
# Ouvrir un template dans votre navigateur
open dashboard-modern/index.html

# Ou avec un serveur local (recommandé)
python3 -m http.server 8000
# Puis visiter : http://localhost:8000/dashboard-modern/
```

## Utiliser un template existant

### Option A : Copie directe

```bash
# Copier un template vers votre projet
cp -r dashboard-modern /chemin/vers/votre/projet/

# Le template est prêt à l'emploi avec :
# ✅ Tailwind CSS via CDN
# ✅ Alpine.js pour l'interactivité
# ✅ ApexCharts pour les graphiques
```

### Option B : Intégration dans un projet existant

1. **Copier le HTML** du template
2. **Installer Tailwind CSS** dans votre projet (si pas déjà fait)
3. **Adapter** les classes Tailwind à votre configuration
4. **Personnaliser** couleurs et contenu

### Personnalisation rapide

Chaque template utilise Tailwind CSS. Pour personnaliser :

```html
<!-- Exemple : Changer les couleurs -->
<!-- Avant : -->
<div class="bg-blue-500 text-white">

<!-- Après : -->
<div class="bg-purple-500 text-white">
```

**Voir la documentation Tailwind :** https://tailwindcss.com/docs

## Créer avec Claude Code

La vraie puissance de ce projet vient de l'utilisation avec **Claude Code**.

### Prérequis

1. **Claude Code installé** → [Guide d'installation](CLAUDE-CODE-GUIDE.md#installation)
2. **Ce repository cloné** localement

### Créer un nouveau composant en 30 secondes

```bash
# 1. Lancer Claude Code dans le repository
cd .context-designs
# (Claude Code doit être actif)

# 2. Donner un prompt simple :
"Crée une carte de produit avec image, titre, description, prix et bouton.
Suis le design system dans .context/ et rends-le accessible."

# 3. Claude Code génère instantanément :
# ✅ Code HTML sémantique
# ✅ Classes Tailwind cohérentes avec le design system
# ✅ Attributs d'accessibilité (ARIA)
# ✅ Design responsive
# ✅ Documentation inline
```

### Pourquoi ça fonctionne si bien ?

Le dossier `.context/` contient toute la documentation de votre design system :

```
.context/
├── styling/design-system.md    → Couleurs, typographie, espacements
├── components/patterns.md      → Structure des composants
├── components/accessibility.md → Standards d'accessibilité
└── ...
```

**Claude Code lit automatiquement cette documentation** et génère du code qui suit VOS standards, pas des standards génériques.

## Guides détaillés

### Pour aller plus loin :

- **[Guide Claude Code](CLAUDE-CODE-GUIDE.md)** - Utiliser Claude Code avec ce projet
- **[Guide Claude Desktop](CLAUDE-DESKTOP-GUIDE.md)** - Utiliser avec Claude Desktop
- **[Guide des Templates](TEMPLATE-GUIDE.md)** - Créer, modifier, et maintenir des templates
- **[README principal](README.md)** - Philosophie et méthodologie complète

## 🎯 Cas d'usage rapides

### Je veux juste utiliser un template

1. Ouvrir `dashboard-modern/index.html`
2. Copier le code vers votre projet
3. Personnaliser le contenu et les couleurs

**Temps estimé :** 5 minutes

### Je veux créer un nouveau composant

1. Installer Claude Code
2. Lancer Claude Code dans ce repo
3. Décrire ce que vous voulez
4. Claude Code génère le code

**Temps estimé :** 2 minutes

### Je veux créer un template complet

1. Lire le [Guide des Templates](TEMPLATE-GUIDE.md)
2. Utiliser Claude Code pour générer
3. Documenter dans le README du template
4. Ajouter un screenshot

**Temps estimé :** 30-60 minutes

## 🆘 Besoin d'aide ?

- **Documentation :** Lire les guides dans `docs/` ou les fichiers `*-GUIDE.md`
- **Exemples :** Explorer les templates existants
- **Issues GitHub :** Ouvrir une issue si vous rencontrez un problème
- **Claude Code :** Poser vos questions directement à Claude Code dans le repo !

## 📚 Structure du projet

```
.context-designs/
├── QUICKSTART.md              ← Vous êtes ici !
├── CLAUDE-CODE-GUIDE.md       ← Guide Claude Code
├── CLAUDE-DESKTOP-GUIDE.md    ← Guide Claude Desktop
├── TEMPLATE-GUIDE.md          ← Guide des templates
├── README.md                  ← Documentation complète
│
├── .context/                  ← Documentation du design system
│   ├── substrate.md
│   ├── architecture/
│   ├── components/
│   ├── styling/
│   └── templates/
│
├── dashboard-modern/          ← Template : Dashboard moderne
├── landing-page-fintech/      ← Template : Landing page fintech
├── dashboard-leads/           ← Template : Dashboard leads
└── ...                        ← Autres templates
```

## 🚀 Prochaines étapes

1. ✅ **Explorez un template** → Ouvrir `dashboard-modern/index.html`
2. ✅ **Lisez le guide Claude Code** → [CLAUDE-CODE-GUIDE.md](CLAUDE-CODE-GUIDE.md)
3. ✅ **Créez votre premier composant** → Utiliser Claude Code avec ce repo
4. ✅ **Partagez vos créations** → Contribuer un nouveau template !

---

**Bon développement !** 🎨✨
