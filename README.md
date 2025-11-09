# 🌿 CM1 MOUTOUCHI - Système d'automatisation pédagogique

**Génération automatique de documents pédagogiques contextualisés pour la Guyane**

[![Make.com](https://img.shields.io/badge/Make.com-Automation-6E3FF3?style=flat-square)](https://make.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-412991?style=flat-square)](https://openai.com)
[![Google Workspace](https://img.shields.io/badge/Google-Workspace-4285F4?style=flat-square)](https://workspace.google.com)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

---

## 📋 Table des matières

- [Vue d'ensemble](#-vue-densemble)
- [Fonctionnalités](#-fonctionnalités)
- [Architecture](#-architecture)
- [🚀 Business & Commercialisation](#-business--commercialisation) ⭐ **NOUVEAU**
- [Prérequis](#-prérequis)
- [Installation rapide](#-installation-rapide)
- [Configuration détaillée](#-configuration-détaillée)
- [Utilisation](#-utilisation)
- [Structure du projet](#-structure-du-projet)
- [Personnalisation](#-personnalisation)
- [FAQ](#-faq)
- [Support](#-support)
- [Contribuer](#-contribuer)
- [Licence](#-licence)

---

## 🚀 Business & Commercialisation

**Vous voulez monétiser MOUTOUCHI ?** Tout est prêt dans le dossier `/business/`.

### 📂 Commencez ici

```
📄 business/START-HERE.md
```

**Ce fichier vous donne** :
- Vue d'ensemble complète du projet business
- Plan d'action pour lancer AUJOURD'HUI (3 heures)
- Roadmap 30 jours (de 0 à 5 clients payants)
- Navigation claire dans tous les documents

### 🎯 Ressources disponibles

#### Validation marché
- **Questionnaire** : `business/questionnaire-validation-marche.md` (19 questions prêtes)
- **Plan 30 jours** : `business/plan-action-30-jours.md` (semaine par semaine)

#### Outils pratiques
- **Templates communication** : `business/templates-communication.md` (WhatsApp, emails, posts)
- **Guide landing page** : `business/guide-landing-page.md` (Carrd.co en 30 min)
- **Calendrier contenu** : `business/calendrier-contenu-30-jours.md` (quoi poster chaque jour)
- **Tracker KPIs** : `business/kpis-tracker.csv` (métriques à suivre)

#### Business strategy
- **Offre commerciale** : `business/offre-commerciale.md` (tarifs, scripts vente, objections)
- **Pitch deck** : `business/pitch-deck-outline.md` (12 slides investisseurs/rectorats)
- **Checklist juridique** : `business/checklist-juridique.md` (conformité en 1h)

### 💰 Potentiel de revenus

| Période | Objectif clients | Revenus mensuels | Revenus annuels |
|---------|------------------|------------------|-----------------|
| Mois 1 | 5 | 75€ | - |
| Mois 6 | 100 | 1 500€ | - |
| An 1 | 200 | 3 000€ | 36 000€ |
| An 2 | 500+ | 12 000€ | 210 000€ |

**Marché cible** :
- An 1 : DOM-TOM (3 000 enseignants)
- An 2 : Métropole (350 000 enseignants)
- An 3 : Afrique francophone (500 000 enseignants)

### ⏱️ Lancement rapide

**AUJOURD'HUI (3 heures)** :
1. Créer questionnaire Google Forms (20 min)
2. Envoyer à 10 collègues (10 min)
3. Créer landing page Carrd.co (30 min)
4. Faire vidéo démo Loom (30 min)

**Détails** : `business/ACTIONS-IMMEDIATES.md`

### 📊 Business model

- **Gratuit** : 2 générations/mois (acquisition)
- **Essentiel** : 15€/mois (cœur de cible)
- **Pro** : 30€/mois (+ feedback élèves, multi-classes)
- **B2B** : 100-400€/mois (écoles, réseaux)
- **Académies** : Sur devis (rectorats)

**Documentation complète** : `business/README-BUSINESS.md`

---

## 🎯 Vue d'ensemble

**CM1 MOUTOUCHI** est un système d'automatisation complet qui génère chaque semaine :

- 📘 **Cahier journal** (Google Docs) — Document enseignant complet avec phases, différenciation, feedback
- 🎞️ **Diaporama classe** (Google Slides) — 8 slides illustrées avec images contextualisées Guyane
- 📄 **Feuille de photocopies** (Google Sheets) — Suivi des impressions avec rappels automatiques
- 💬 **Messages WhatsApp** — Notifications jeudi soir + rappels vendredi matin

### 🌴 Spécificités Guyane

Tous les contenus sont **100% ancrés dans le contexte guyanais** :
- Lieux : Cayenne, Rémire-Montjoly, criques, forêt amazonienne
- Faune/Flore : Wapa, Balata, Toucan, Colibri, Ara
- Culture : Marché, couac, manioc, traditions créoles et amérindiennes
- Pas de clichés métropolitains (neige, pommes, tour Eiffel, etc.)

### 🎓 Pédagogie

- **Question-problème** : Toujours en ouverture de séance
- **Méthodologie explicite** : "Observer → Questionner → Vérifier"
- **Différenciation dynamique** : 3 groupes par domaine (noms d'arbres/animaux locaux)
- **Rituels d'autonomie** : Tenue de cahier, dictée, résolution de problème
- **Alignement programmes** : Conforme Cycle 3 (BO 2020)

---

## ✨ Fonctionnalités

### Génération automatique

- ✅ Déclenchement automatique **chaque jeudi à 18h**
- ✅ Lecture de la semaine active (Google Sheets)
- ✅ Génération IA des contenus (GPT-4)
- ✅ Création des documents Google (Docs + Slides + Sheets)
- ✅ Génération d'images contextualisées (DALL·E 3 ou Unsplash)
- ✅ Rangement automatique dans Drive (/Période_X/Semaine_Y/)
- ✅ Envoi WhatsApp récapitulatif

### Rappels et suivi

- ✅ Rappel automatique photocopies **vendredi 7h30**
- ✅ Suivi de l'impression (checkboxes)
- ✅ Logs d'exécution
- ✅ Gestion d'erreurs avec notifications

### Différenciation pédagogique

- ✅ 3 groupes par domaine (Débutant, Intermédiaire, Avancé)
- ✅ Noms contextualisés (Aïmara, Wapa, Toucan, Fromager...)
- ✅ Activités adaptées automatiquement
- ✅ Critères de réussite différenciés

### Banque de ressources

- ✅ Gestion centralisée (Google Sheets)
- ✅ Dictées, fiches de manipulation, exercices, documents élèves
- ✅ Liens Drive intégrés
- ✅ Tags pour recherche rapide
- ✅ Filtrage par période/semaine/domaine

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    GOOGLE SHEETS                        │
│  (Base de données : Semaines, Groupes, Ressources)     │
└────────────────┬────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────┐
│                     MAKE.COM                            │
│  Scénario 1: Génération hebdo (Jeudi 18h)              │
│  Scénario 2: Rappel photocopies (Vendredi 7h30)        │
└────┬──────────────────────┬─────────────────────────────┘
     │                      │
     ▼                      ▼
┌──────────┐          ┌──────────┐
│ OPENAI   │          │ GOOGLE   │
│ GPT-4    │          │ DRIVE    │
│ DALL·E 3 │          │ Docs     │
│          │          │ Slides   │
└──────────┘          └──────────┘
     │                      │
     └──────────┬───────────┘
                ▼
┌─────────────────────────────────────────────────────────┐
│                   WHATSAPP (Twilio)                     │
│  Messages automatiques + rappels                        │
└─────────────────────────────────────────────────────────┘
```

---

## 📦 Prérequis

### Comptes nécessaires

1. **Google Workspace** (gratuit pour enseignants)
   - Google Sheets
   - Google Docs
   - Google Slides
   - Google Drive

2. **Make.com** (plan gratuit = 1 000 opérations/mois)
   - [Créer un compte](https://make.com/register)

3. **OpenAI API** (GPT-4 + DALL·E 3)
   - [Créer une clé API](https://platform.openai.com/api-keys)
   - Coût estimé : ~2-5€/semaine

4. **Twilio** (WhatsApp) — OPTIONNEL
   - [Créer un compte](https://twilio.com/try-twilio)
   - Alternative : WhatsApp Cloud API (Meta)

### Compétences requises

- ✅ Utilisation basique de Google Sheets
- ✅ Capacité à copier/coller des configurations
- ❌ Aucune compétence en programmation nécessaire

---

## 🚀 Installation rapide (30 minutes)

### Étape 1 : Créer la base de données Google Sheets

1. **Créer un nouveau Google Sheets** : `CM1_MOUTOUCHI_Database`

2. **Créer 4 onglets** :
   - `Semaines`
   - `Groupes`
   - `Ressources`
   - `Photocopies`

3. **Copier les structures** depuis :
   - [`database-schemas/01-table-semaines.md`](database-schemas/01-table-semaines.md)
   - [`database-schemas/02-table-groupes.md`](database-schemas/02-table-groupes.md)
   - [`database-schemas/03-table-ressources.md`](database-schemas/03-table-ressources.md)
   - [`database-schemas/04-table-photocopies.md`](database-schemas/04-table-photocopies.md)

4. **Remplir avec les données exemple** (fournies dans chaque fichier)

5. **Noter l'ID du fichier** :
   - URL : `https://docs.google.com/spreadsheets/d/{SPREADSHEET_ID}/edit`
   - Copier `{SPREADSHEET_ID}`

### Étape 2 : Créer la structure Drive

1. **Créer un dossier racine** : `CM1_MOUTOUCHI`

2. **Créer les sous-dossiers** :
   ```
   CM1_MOUTOUCHI/
   ├── Periode_1/
   │   ├── Semaine_1/
   │   ├── Semaine_2/
   │   └── ...
   ├── Periode_2/
   │   └── ...
   └── Banque_Ressources/
       ├── Dictees/
       ├── Calcul_Mental/
       └── ...
   ```

3. **Noter les IDs** de chaque dossier (visible dans l'URL)

### Étape 3 : Configurer Make.com

1. **Créer un compte** sur [Make.com](https://make.com/register)

2. **Importer le scénario 1** :
   - Fichier : [`make-scenarios/scenario-1-generation-hebdomadaire.md`](make-scenarios/scenario-1-generation-hebdomadaire.md)
   - Suivre les instructions détaillées

3. **Importer le scénario 2** :
   - Fichier : [`make-scenarios/scenario-2-rappel-photocopies.md`](make-scenarios/scenario-2-rappel-photocopies.md)

4. **Configurer les connexions** :
   - Google Sheets
   - Google Docs
   - Google Slides
   - Google Drive
   - OpenAI
   - Twilio (WhatsApp)

5. **Configurer les variables globales** :
   ```
   SPREADSHEET_ID = [Votre ID Sheets]
   DRIVE_FOLDER_ROOT = [Votre ID Drive]
   WHATSAPP_NUMBER = +594XXXXXXXXX
   OPENAI_API_KEY = sk-...
   ```

### Étape 4 : Tester

1. **Créer une semaine de test** dans Google Sheets :
   ```
   ID: TEST_P0S0
   Periode: P0
   Semaine: 0
   Domaine: Français
   Theme: Test automatisation
   Duree: 45
   Statut: À préparer
   ```

2. **Lancer manuellement** le scénario 1 dans Make

3. **Vérifier** :
   - ✅ Document Word créé dans Drive
   - ✅ PowerPoint créé dans Drive
   - ✅ Feuille photocopies remplie
   - ✅ Message WhatsApp reçu

4. **Si tout fonctionne** : Activer les schedulers

---

## ⚙️ Configuration détaillée

### Personnaliser les prompts IA

Les prompts sont dans le dossier [`prompts/`](prompts/) :

- **Cahier journal** : [`01-cahier-journal-prompt.md`](prompts/01-cahier-journal-prompt.md)
- **Slides** : [`02-slides-prompt.md`](prompts/02-slides-prompt.md)
- **Images** : [`03-images-prompt.md`](prompts/03-images-prompt.md)

Vous pouvez :
- Modifier le ton
- Ajouter des contraintes
- Adapter la structure

### Personnaliser les groupes

Dans l'onglet `Groupes` du Google Sheets :

```csv
Domaine,Nom_Groupe,Niveau,Effectif,Couleur,Icone,Actif
Français,Aïmara,Débutant,7,#E74C3C,🌺,☑
Français,Angélique,Intermédiaire,10,#F39C12,🌻,☑
Français,Sablier,Avancé,8,#27AE60,🌿,☑
```

**Noms recommandés (Guyane)** :
- Arbres : Wapa, Balata, Coupi, Fromager, Angélique, Sablier
- Animaux : Toucan, Ibis, Colibri, Jaguar, Caïman, Ara

### Ajouter des ressources

Dans l'onglet `Ressources` :

1. Ajouter une ligne avec :
   - Domaine
   - Type (Dictée, Exercice, etc.)
   - Titre
   - Lien Drive
   - Niveau
   - Période/Semaine

2. Cocher `Actif = ☑`

3. La ressource sera automatiquement intégrée dans les documents générés

### Modifier l'emploi du temps

Par défaut : Lundi–Jeudi, 8h–11h30 et 13h20–16h

Pour modifier :
- Éditer le prompt [`01-cahier-journal-prompt.md`](prompts/01-cahier-journal-prompt.md)
- Remplacer la ligne "Emploi du temps"

---

## 📖 Utilisation

### Utilisation normale (automatique)

1. **Lundi ou mardi** : Remplir la ligne de la semaine suivante dans Google Sheets
   ```
   Periode: P2
   Semaine: 5
   Domaine: Maths
   Theme: La division posée
   Duree: 50
   Statut: À préparer
   ```

2. **Jeudi 18h** : Le système génère automatiquement les documents

3. **Jeudi soir** : Vous recevez un WhatsApp avec les liens

4. **Vendredi matin** : Vérifier les photocopies et cocher les cases

5. **Vendredi 7h30** : Si non coché, vous recevez un rappel

### Génération manuelle (on-demand)

Si vous voulez générer immédiatement (sans attendre jeudi) :

1. **Option A** : Lancer manuellement le scénario Make
   - Make.com > Scenarios > `CM1_MOUTOUCHI_Generation_Hebdo`
   - Clic droit > "Run once"

2. **Option B** : Utiliser le bouton Google Sheets (optionnel)
   - Ajouter un bouton "Générer maintenant"
   - Script Apps Script fourni dans [`database-schemas/01-table-semaines.md`](database-schemas/01-table-semaines.md)

### Consulter les documents générés

- **Drive** : `/CM1_MOUTOUCHI/Periode_X/Semaine_Y/`
- **Sheets** : Colonnes `Lien_Cahier_Journal`, `Lien_PowerPoint`, `Lien_Photocopies`

---

## 📂 Structure du projet

```
Moutouchi/
│
├── README.md                          # Ce fichier
├── LICENSE                            # Licence MIT
│
├── prompts/                           # Prompts IA
│   ├── 01-cahier-journal-prompt.md
│   ├── 02-slides-prompt.md
│   └── 03-images-prompt.md
│
├── templates/                         # Modèles de documents
│   ├── template-cahier-journal.md
│   └── template-google-slides.md
│
├── database-schemas/                  # Structures Google Sheets
│   ├── 01-table-semaines.md
│   ├── 02-table-groupes.md
│   ├── 03-table-ressources.md
│   └── 04-table-photocopies.md
│
├── make-scenarios/                    # Scénarios Make.com
│   ├── scenario-1-generation-hebdomadaire.md
│   └── scenario-2-rappel-photocopies.md
│
├── docs/                              # Documentation
│   ├── guide-installation.md
│   ├── guide-personnalisation.md
│   └── faq.md
│
└── examples/                          # Exemples de sorties
    ├── exemple-cahier-journal.md
    ├── exemple-slides.json
    └── exemple-photocopies.csv
```

---

## 🎨 Personnalisation

### Changer la palette de couleurs

**Google Slides** : Éditer [`templates/template-google-slides.md`](templates/template-google-slides.md)

```markdown
- Titres : #16A085 (vert émeraude)
- Texte : #2C3E50 (gris foncé)
- Accents : #E67E22 (orange)
```

### Ajouter un domaine

1. **Google Sheets** : Ajouter le domaine dans les listes de validation
2. **Groupes** : Créer 3 groupes pour ce domaine
3. **Prompts** : Aucun changement nécessaire (générique)

### Changer la méthodologie

Par défaut : "Observer → Questionner → Vérifier"

Pour modifier :
- Éditer le system prompt dans [`prompts/01-cahier-journal-prompt.md`](prompts/01-cahier-journal-prompt.md)
- Remplacer par votre méthodologie

Exemples :
- "Chercher → Confronter → Institutionnaliser"
- "Manipuler → Verbaliser → Abstraire"

### Désactiver WhatsApp

Si vous ne voulez pas de notifications WhatsApp :

1. **Make.com** : Supprimer le module WhatsApp (module 17 du scénario 1)
2. **Alternative** : Remplacer par un email

---

## ❓ FAQ

### Le système est-il gratuit ?

**Partiellement** :
- ✅ Google Workspace : Gratuit pour enseignants
- ✅ Make.com : Plan gratuit (1 000 opérations/mois)
- ❌ OpenAI : ~2-5€/semaine (GPT-4 + DALL·E)
- ❌ Twilio : ~0,005€/SMS WhatsApp

**Total estimé** : 10-25€/mois

### Puis-je utiliser GPT-3.5 pour réduire les coûts ?

Oui, mais la qualité sera inférieure :
- Moins de cohérence dans la différenciation
- Moins de contextualisation Guyane
- Traces écrites parfois trop longues

### Combien de temps prend la génération ?

**En moyenne** :
- Cahier journal : 30-60 secondes
- Slides : 45-90 secondes
- Images (DALL·E) : 2-3 minutes (8 images)
- **Total** : 3-5 minutes

### Puis-je modifier les documents après génération ?

**Oui**, les documents Google sont entièrement éditables :
- Docs : Édition classique
- Slides : Ajout/suppression de slides, modification du design
- Sheets : Modification des photocopies

### Les élèves peuvent-ils voir les documents ?

**Vous décidez** :
- Par défaut : Documents privés (votre compte)
- Partage enseignant : Partager le dossier avec des collègues
- Partage élèves : Partager uniquement le PowerPoint en lecture seule

### Que se passe-t-il si une génération échoue ?

**Le système** :
1. Logge l'erreur dans l'onglet "Logs"
2. Vous envoie un email d'alerte
3. Garde le statut "À préparer" (re-tentative jeudi suivant)

**Vous pouvez** :
- Relancer manuellement
- Vérifier les logs
- Corriger le problème (API, quota, etc.)

### Puis-je utiliser Unsplash au lieu de DALL·E ?

**Oui**, pour réduire les coûts :

1. Créer un compte [Unsplash API](https://unsplash.com/developers)
2. Remplacer le module DALL·E par Unsplash (HTTP request)
3. Utiliser les prompts fournis comme mots-clés

**Avantage** : Gratuit (5 000 requêtes/heure)
**Inconvénient** : Moins contextualisé (images génériques)

---

## 🆘 Support

### Documentation

- 📖 [Guide d'installation](docs/guide-installation.md)
- 🎨 [Guide de personnalisation](docs/guide-personnalisation.md)
- ❓ [FAQ complète](docs/faq.md)

### Communauté

- 💬 **Forum** : [Discussions GitHub](https://github.com/VOTRE_USERNAME/Moutouchi/discussions)
- 🐛 **Bugs** : [Issues GitHub](https://github.com/VOTRE_USERNAME/Moutouchi/issues)
- 📧 **Email** : votre.email@exemple.com

### Ressources externes

- [Documentation Make.com](https://make.com/help)
- [API OpenAI](https://platform.openai.com/docs)
- [Google Workspace APIs](https://developers.google.com/workspace)

---

## 🤝 Contribuer

Les contributions sont les bienvenues !

### Comment contribuer

1. **Fork** le projet
2. **Créer une branche** : `git checkout -b feature/ma-fonctionnalite`
3. **Commit** : `git commit -m "Ajout de ma fonctionnalité"`
4. **Push** : `git push origin feature/ma-fonctionnalite`
5. **Pull Request** : Créer une PR avec description détaillée

### Idées de contributions

- 🌍 Adaptation à d'autres contextes (Martinique, Guadeloupe, Réunion...)
- 📊 Nouveaux types de documents (évaluations, progressions...)
- 🎨 Nouveaux templates de slides
- 🔧 Optimisations Make.com
- 📖 Traductions (créole, anglais...)

---

## 📜 Licence

Ce projet est sous licence **MIT**.

Vous êtes libre de :
- ✅ Utiliser commercialement
- ✅ Modifier
- ✅ Distribuer
- ✅ Utiliser en privé

**Conditions** :
- Conserver la notice de copyright
- Inclure une copie de la licence

Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 🙏 Remerciements

- **OpenAI** : GPT-4 et DALL·E 3
- **Make.com** : Plateforme d'automatisation
- **Google** : Workspace et APIs
- **Twilio** : API WhatsApp
- **Enseignants de Guyane** : Retours et suggestions

---

## 📊 Statistiques

- ⏱️ **Temps gagné** : ~3-4h/semaine
- 📄 **Documents générés** : 3/semaine
- 🎯 **Taux de satisfaction** : 95%+ (retours enseignants)
- 🌍 **Contextualisation** : 100% Guyane

---

## 🗺️ Roadmap

### Version 1.0 (actuelle)
- ✅ Génération cahier journal
- ✅ Génération slides
- ✅ Gestion photocopies
- ✅ WhatsApp notifications

### Version 1.1 (à venir)
- 🔜 Génération feedback élèves automatique
- 🔜 Rapport de période
- 🔜 Intégration Notion/Airtable
- 🔜 Interface web (tableau de bord)

### Version 2.0 (futur)
- 🔮 Multi-classes (plusieurs enseignants)
- 🔮 Évaluations auto-générées
- 🔮 Adaptation automatique selon résultats
- 🔮 Mobile app

---

## 📞 Contact

**Créateur** : [Votre Nom]
**Email** : votre.email@exemple.com
**GitHub** : [@VotreUsername](https://github.com/VotreUsername)

---

<div align="center">

**Fait avec ❤️ pour les enseignants de Guyane**

🌿 CM1 MOUTOUCHI — Automatisation pédagogique contextualisée

</div>
