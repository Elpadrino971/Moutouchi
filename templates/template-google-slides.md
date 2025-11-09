# MODÈLE GOOGLE SLIDES CM1 MOUTOUCHI

> **Ce document décrit la structure des 8 slides à créer automatiquement**
> Utilisation : Google Slides API via Make.com

---

## STRUCTURE GÉNÉRALE

- **Format** : 16:9 (1920x1080 ou 1280x720)
- **Nombre de slides** : 8 fixes
- **Police** : Roboto ou Open Sans (lisible, sans serif)
- **Taille de police** :
  - Titre : 44pt
  - Corps : 28pt
  - Notes : 20pt
- **Couleurs** :
  - Texte principal : #2C3E50 (gris foncé)
  - Titres : #16A085 (vert émeraude)
  - Accents : #E67E22 (orange)
  - Fond texte : blanc avec opacité 85% (pour lisibilité sur image)

---

## SLIDE 1 : Question d'ouverture

### Layout
```
┌─────────────────────────────────────┐
│                                     │
│   QUESTION D'OUVERTURE              │ ← Titre (vert #16A085)
│                                     │
│   {{QUESTION_TEXT}}                 │ ← Corps (gris #2C3E50, grande taille)
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
     [Image de fond : classe Guyane]
```

### Variables Make
- `{{slide1.title}}` → Text placeholder "Title"
- `{{slide1.text}}` → Text placeholder "Body"
- `{{slide1.bg_prompt}}` → Background image (via DALL·E/Unsplash)

### Configuration API
```json
{
  "requests": [
    {
      "createSlide": {
        "slideLayoutReference": {"predefinedLayout": "TITLE_AND_BODY"}
      }
    },
    {
      "insertText": {
        "objectId": "title_id",
        "text": "{{slide1.title}}"
      }
    },
    {
      "insertText": {
        "objectId": "body_id",
        "text": "{{slide1.text}}"
      }
    }
  ]
}
```

---

## SLIDE 2 : Mise en recherche

### Layout
```
┌─────────────────────────────────────┐
│ MISE EN RECHERCHE                   │
│                                     │
│ • {{bullet_point_1}}                │
│ • {{bullet_point_2}}                │
│ • {{bullet_point_3}}                │
│                                     │
│ 👥 Travail en binômes + tuteurs     │
└─────────────────────────────────────┘
     [Image de fond : élèves en groupe]
```

### Variables Make
- `{{slide2.title}}` → Titre
- `{{slide2.bullet_points}}` → Array de 3-4 points
- `{{slide2.bg_prompt}}` → Image de fond

---

## SLIDE 3 : Méthode du jour

### Layout
```
┌─────────────────────────────────────┐
│ MÉTHODE DU JOUR                     │
│                                     │
│ 1️⃣ {{step_1}}                      │
│ 2️⃣ {{step_2}}                      │
│ 3️⃣ {{step_3}}                      │
│                                     │
│ 💡 Rappel : {{teacher_tip}}         │
└─────────────────────────────────────┘
     [Image de fond : affiche méthodo]
```

### Variables Make
- `{{slide3.title}}` → Titre
- `{{slide3.steps}}` → Array de 3 étapes (liste numérotée)
- `{{slide3.teacher_tip}}` → Conseil enseignant (text box en bas)
- `{{slide3.bg_prompt}}` → Image de fond

### Particularité
- Utiliser une **liste numérotée** (format API différent)
- Text box supplémentaire en bas pour le "teacher_tip"

---

## SLIDE 4 : Confrontation collective

### Layout
```
┌─────────────────────────────────────┐
│ CONFRONTATION COLLECTIVE            │
│                                     │
│ ❓ {{question_1}}                   │
│                                     │
│ ❓ {{question_2}}                   │
│                                     │
│ ❓ {{question_3}}                   │
└─────────────────────────────────────┘
     [Image de fond : tableau + élèves]
```

### Variables Make
- `{{slide4.title}}` → Titre
- `{{slide4.bullet_points}}` → Array de questions
- `{{slide4.bg_prompt}}` → Image de fond

---

## SLIDE 5 : Bilan (trace collective)

### Layout
```
┌─────────────────────────────────────┐
│ BILAN                               │
│                                     │
│                                     │
│   {{trace_ecrite_text}}             │ ← Centré, grande taille
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
     [Image de fond : cahier ouvert]
```

### Variables Make
- `{{slide5.title}}` → Titre
- `{{slide5.text}}` → Texte de la trace écrite (2-3 phrases)
- `{{slide5.bg_prompt}}` → Image de fond

### Particularité
- Texte centré verticalement et horizontalement
- Police légèrement plus grande (32pt)
- Encadré avec fond blanc opaque pour lisibilité

---

## SLIDE 6 : Rituels d'autonomie

### Layout
```
┌─────────────────────────────────────┐
│ RITUELS D'AUTONOMIE                 │
│                                     │
│ ✅ {{checklist_item_1}}             │
│ ✅ {{checklist_item_2}}             │
│ ✅ {{checklist_item_3}}             │
│                                     │
└─────────────────────────────────────┘
     [Image de fond : bureau rangé]
```

### Variables Make
- `{{slide6.title}}` → Titre
- `{{slide6.checklist}}` → Array de 3 items (tenue cahier, dictée, problème)
- `{{slide6.bg_prompt}}` → Image de fond

### Particularité
- Utiliser des emojis ✅ pour les checkboxes
- Format bullet list

---

## SLIDE 7 : Activité différenciée par groupes

### Layout
```
┌─────────────────────────────────────┐
│ ACTIVITÉ PAR GROUPES                │
│                                     │
│ ┌───────────────┬─────────────────┐ │
│ │ Groupe        │ {{group_1_name}}│ │
│ │ Activité      │ {{group_1_task}}│ │
│ │ Réussite      │ {{group_1_crit}}│ │
│ ├───────────────┼─────────────────┤ │
│ │ [Groupe 2]    │ ...             │ │
│ ├───────────────┼─────────────────┤ │
│ │ [Groupe 3]    │ ...             │ │
│ └───────────────┴─────────────────┘ │
└─────────────────────────────────────┘
     [Image de fond : groupes travaillant]
```

### Variables Make
- `{{slide7.title}}` → Titre
- `{{slide7.groups}}` → Array d'objets :
  ```json
  [
    {"name": "Aïmara", "task": "...", "success_criteria": "..."},
    {"name": "Angélique", "task": "...", "success_criteria": "..."},
    {"name": "Sablier", "task": "...", "success_criteria": "..."}
  ]
  ```
- `{{slide7.bg_prompt}}` → Image de fond

### Particularité
- Utiliser une **table** (API `createTable`)
- 3 lignes (1 par groupe) × 3 colonnes (nom, activité, critère)
- Alternance de couleurs de lignes pour lisibilité

---

## SLIDE 8 : Feedback & suite

### Layout
```
┌─────────────────────────────────────┐
│ FEEDBACK & SUITE                    │
│                                     │
│ 📚 Ce qu'on a appris :              │
│    {{learned_text}}                 │
│                                     │
│ 🎯 Demain on travaillera sur :      │
│    {{next_text}}                    │
│                                     │
└─────────────────────────────────────┘
     [Image de fond : coucher de soleil]
```

### Variables Make
- `{{slide8.title}}` → Titre
- `{{slide8.bullet_points}}` → Array de 2 éléments (appris, à venir)
- `{{slide8.bg_prompt}}` → Image de fond

---

## INSTRUCTIONS DE GÉNÉRATION MAKE.COM

### Étape 1 : Créer la présentation

**Module** : Google Slides > Create a Presentation

**Configuration** :
- **Title** : `CM1_{{PERIODE}}_{{SEMAINE}}_{{DOMAINE}}`
- **Folder** : ID du dossier Drive cible

**Sortie** : `{{presentation_id}}`

---

### Étape 2 : Pour chaque slide (boucle 1-8)

**Module** : Google Slides > Make an API Call

**Endpoint** : `presentations.batchUpdate`

**Body** :
```json
{
  "requests": [
    {
      "createSlide": {
        "slideLayoutReference": {"predefinedLayout": "TITLE_AND_BODY"}
      }
    }
  ]
}
```

---

### Étape 3 : Remplir le contenu de chaque slide

**Module** : Google Slides > Replace Text

**Configuration** :
- **Presentation ID** : `{{presentation_id}}`
- **Page Object ID** : `{{slide_object_id}}`
- **Replace Text** : Mappage des variables JSON

---

### Étape 4 : Insérer les images de fond

**Module** : Google Slides > Make an API Call

**Endpoint** : `presentations.batchUpdate`

**Body** :
```json
{
  "requests": [
    {
      "updatePageProperties": {
        "objectId": "{{slide_object_id}}",
        "pageProperties": {
          "pageBackgroundFill": {
            "stretchedPictureFill": {
              "contentUrl": "{{image_url}}"
            }
          }
        },
        "fields": "pageBackgroundFill"
      }
    }
  ]
}
```

---

## PALETTE DE COULEURS RECOMMANDÉE

| Élément | Couleur HEX | Utilisation |
|---------|-------------|-------------|
| Titres | `#16A085` | Vert émeraude (évoque la forêt guyanaise) |
| Texte principal | `#2C3E50` | Gris foncé (lisible) |
| Accents | `#E67E22` | Orange (touche de couleur) |
| Fond texte | `#FFFFFF` (opacité 85%) | Blanc semi-transparent |
| Tableaux (ligne 1) | `#ECF0F1` | Gris très clair |
| Tableaux (ligne 2) | `#FFFFFF` | Blanc |

---

## CHECKLIST AVANT GÉNÉRATION

- ✅ Les 8 slides sont créées dans l'ordre
- ✅ Toutes les variables JSON sont remplies
- ✅ Les images de fond sont générées et insérées
- ✅ La police est lisible (Roboto/Open Sans)
- ✅ Le contraste texte/fond est suffisant
- ✅ Les groupes correspondent à `{{GROUPS_JSON}}`
- ✅ Aucune référence non-locale (neige, pommes, etc.)

---

**Template créé pour le système CM1 MOUTOUCHI**
*Version 1.0 - Compatible Google Slides API*
