# Prompt IA — Slides (Google Slides)

**But** : générer le contenu textuel de 8 slides (injection dans Google Slides). Inclure la question d'ouverture, la méthode, les activités différenciées, les rituels et un bilan. Prévoir descripteurs d'image pour fonds d'écran libres/IA.

**Modèle Make** – OpenAI (gpt-4/4.1/4o)

---

## SYSTEM PROMPT

```
Tu génères le contenu exact de 8 diapositives pédagogiques CM1, centrées réflexion/méthodo, ancrées en Guyane, sans jargon ni remplissage.

Toujours commencer par une question-problème.

Retourne du JSON strict, clés figées, pas de texte hors JSON.
```

---

## USER PROMPT (avec variables)

```
Variables :
- Domaine : {{DOMAINE}}
- Thème : {{THEME}}
- Période/Semaine : {{PERIODE}}/{{SEMAINE}}
- Groupes : {{GROUPS_JSON}}
- Contrainte : images/fonds = contexte Guyane (libres de droit ou IA)

Retourne un JSON avec EXACTEMENT ces clés :

{
  "slide1": {
    "title": "Question d'ouverture",
    "text": "… (1 à 2 phrases, question-problème Guyane)",
    "bg_prompt": "descripteur image/fond (ex: salle de classe en Guyane, lumière naturelle, carte de la Guyane au tableau)"
  },
  "slide2": {
    "title": "Mise en recherche (binômes / tuteurs)",
    "bullet_points": ["…","…"],
    "bg_prompt": "…"
  },
  "slide3": {
    "title": "Méthode du jour",
    "steps": ["Observer", "Questionner", "Vérifier"],
    "teacher_tip": "Rappel bref à projeter",
    "bg_prompt": "…"
  },
  "slide4": {
    "title": "Confrontation collective",
    "bullet_points": ["Question guidée 1", "Question guidée 2"],
    "bg_prompt": "…"
  },
  "slide5": {
    "title": "Bilan (trace collective)",
    "text": "2-3 phrases courtes et justes",
    "bg_prompt": "…"
  },
  "slide6": {
    "title": "Rituels d'autonomie",
    "checklist": ["Tenue du cahier : …", "Dictée : écouter → relire → corriger", "Problème : lire 2x → schéma → calcul → vérifier"],
    "bg_prompt": "…"
  },
  "slide7": {
    "title": "Activité différenciée par groupes",
    "groups": [
      {"name":"…","task":"…","success_criteria":"…"},
      {"name":"…","task":"…","success_criteria":"…"},
      {"name":"…","task":"…","success_criteria":"…"}
    ],
    "bg_prompt": "…"
  },
  "slide8": {
    "title": "Feedback & suite",
    "bullet_points": ["Ce qu'on a appris…", "Ce qu'on fera mieux demain…"],
    "bg_prompt": "…"
  }
}
```

---

## VARIABLES REQUISES (Make.com)

| Variable | Type | Exemple | Source |
|----------|------|---------|--------|
| `{{DOMAINE}}` | String | "Français" | Google Sheets - Colonne "Domaine" |
| `{{THEME}}` | String | "Identifier le groupe sujet" | Google Sheets - Colonne "Thème" |
| `{{PERIODE}}` | String | "P2" | Google Sheets - Colonne "Période" |
| `{{SEMAINE}}` | String | "S4" | Google Sheets - Colonne "Semaine" |
| `{{GROUPS_JSON}}` | JSON | `{"fr":["Aïmara","Angélique","Sablier"]}` | Google Sheets - Table "Groupes" |

---

## EXEMPLE DE SORTIE ATTENDUE

```json
{
  "slide1": {
    "title": "Question d'ouverture",
    "text": "Dans la phrase 'Le wapa pousse près des criques', qui fait l'action de pousser ?",
    "bg_prompt": "salle de classe CM1 en Guyane, tableau vert, lumière naturelle venant de grandes fenêtres, carte de la Guyane affichée, ambiance lumineuse et aérée"
  },
  "slide2": {
    "title": "Mise en recherche (binômes / tuteurs)",
    "bullet_points": [
      "Manipuler les bandes-phrases",
      "Isoler le mot ou groupe de mots qui fait l'action",
      "Discuter avec votre binôme : êtes-vous d'accord ?"
    ],
    "bg_prompt": "élèves de CM1 en binôme autour d'une table en bois, manipulant des étiquettes de papier, lumière douce, environnement tropical visible par la fenêtre"
  },
  "slide3": {
    "title": "Méthode du jour",
    "steps": ["Observer la phrase", "Questionner : qui fait l'action ?", "Vérifier en changeant le temps du verbe"],
    "teacher_tip": "Rappel : on cherche QUI ou QUOI fait l'action du verbe",
    "bg_prompt": "affiche méthodologique sur mur de classe guyanaise, fond neutre beige, écriture claire, ambiance professionnelle et sereine"
  },
  "slide4": {
    "title": "Confrontation collective",
    "bullet_points": [
      "Quel groupe de mots avez-vous trouvé ?",
      "Comment avez-vous fait pour le trouver ?",
      "Quelqu'un a trouvé différemment ?"
    ],
    "bg_prompt": "tableau blanc avec phrases écrites en grand, main d'enseignant soulignant un mot, classe floue en arrière-plan, lumière naturelle"
  },
  "slide5": {
    "title": "Bilan (trace collective)",
    "text": "Le groupe sujet fait l'action du verbe. Pour le trouver, je pose la question 'Qui fait l'action ?' ou 'Qu'est-ce qui fait l'action ?'.",
    "bg_prompt": "cahier d'écolier ouvert sur table en bois, écriture soignée visible, crayon posé à côté, fond flou aux tons chauds"
  },
  "slide6": {
    "title": "Rituels d'autonomie",
    "checklist": [
      "Tenue du cahier : date soulignée, titre encadré, saut de ligne avant trace",
      "Dictée : écouter → écrire → relire → corriger au stylo vert",
      "Problème : lire 2x → chercher données → schéma → calcul → vérifier"
    ],
    "bg_prompt": "bureau d'écolier bien rangé, ardoise, cahier, trousse alignés, vue de dessus, lumière douce, tons neutres et professionnels"
  },
  "slide7": {
    "title": "Activité différenciée par groupes",
    "groups": [
      {
        "name": "Aïmara",
        "task": "Phrases courtes (sujet = nom propre)",
        "success_criteria": "5/5 sujets identifiés correctement"
      },
      {
        "name": "Angélique",
        "task": "Phrases moyennes (sujet = groupe nominal)",
        "success_criteria": "4/5 + justification orale"
      },
      {
        "name": "Sablier",
        "task": "Phrases complexes (inversion, relative)",
        "success_criteria": "3/5 + reformulation"
      }
    ],
    "bg_prompt": "trois groupes d'élèves distincts, chacun à une table différente, travaillant de manière concentrée, classe lumineuse en Guyane, ambiance collaborative"
  },
  "slide8": {
    "title": "Feedback & suite",
    "bullet_points": [
      "Aujourd'hui, nous avons appris à identifier le groupe sujet",
      "Demain, nous travaillerons sur l'accord du verbe avec le sujet"
    ],
    "bg_prompt": "soleil couchant à travers fenêtre de classe en Guyane, ambiance calme de fin de journée, tableau en arrière-plan, teintes chaudes et apaisantes"
  }
}
```

---

## INTÉGRATION DANS GOOGLE SLIDES (Make.com)

### Mappage des champs JSON vers Slides

| Slide | Élément JSON | Type de shape Slides | Action Make |
|-------|--------------|---------------------|-------------|
| 1 | `slide1.title` | Text placeholder "Title" | Replace text |
| 1 | `slide1.text` | Text placeholder "Body" | Replace text |
| 1 | `slide1.bg_prompt` | Background image | Generate image → Set background |
| 2 | `slide2.bullet_points` | Bullet list placeholder | Create bulleted list |
| 3 | `slide3.steps` | Numbered list | Create numbered list |
| 3 | `slide3.teacher_tip` | Text box (bottom) | Create text box |
| 7 | `slide7.groups` | Table 3x3 | Create table, populate cells |

### Module Make recommandé

```
Google Slides API > presentations.batchUpdate
```

**Actions à enchaîner :**
1. Créer présentation depuis template
2. Pour chaque slide : remplacer textes
3. Pour chaque `bg_prompt` : appeler DALL·E/Unsplash → insérer image background
4. Sauvegarder dans Drive

---

## CHECKLIST QUALITÉ (à intégrer dans Make)

- ✅ Slide 1 contient une question-problème
- ✅ Tous les `bg_prompt` sont contextualisés Guyane
- ✅ Slide 6 contient les 3 rituels (cahier, dictée, problème)
- ✅ Slide 7 contient autant de groupes que dans `{{GROUPS_JSON}}`
- ✅ Aucune référence non-locale (neige, pommes, etc.)
- ✅ JSON valide (pas de texte hors structure)
