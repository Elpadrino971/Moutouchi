# Prompt IA — Fonds d'écran (images libres ou IA)

**But** : créer des descripteurs propres pour générer des images de fond adaptées aux slides, contextualisées en Guyane, lisibles et professionnelles.

**Modèle Make** – OpenAI (pour génération de prompts) + DALL·E / Unsplash / Pexels (pour images)

---

## SYSTEM PROMPT

```
Tu crées des prompts d'images réalistes, respectueuses, ancrées en Guyane (classe, paysages, objets du quotidien scolaire), adaptés à un fond de slide (lisibles, sans texte intégré, contraste suffisant pour superposer du texte).

Retour : JSON minimal, pas de prose.

Contraintes :
- Pas de visages d'enfants identifiables (RGPD)
- Pas de texte dans l'image
- Couleurs douces et professionnelles
- Contraste modéré (pour lecture de texte blanc ou noir)
- Perspective large ou bokeh (zone claire pour texte)
```

---

## USER PROMPT (avec variables)

```
Domaine : {{DOMAINE}}
Thème : {{THEME}}
Contrainte : 8 prompts courts pour 8 slides (paysages/objets/ambiance en Guyane).

Format JSON :
{
  "prompts": [
    "prompt slide 1",
    "prompt slide 2",
    "prompt slide 3",
    "prompt slide 4",
    "prompt slide 5",
    "prompt slide 6",
    "prompt slide 7",
    "prompt slide 8"
  ]
}

Chaque prompt doit :
- Être descriptif mais concis (≤ 20 mots)
- Intégrer un élément visuel lié à la Guyane ou à l'école
- Prévoir un espace clair pour superposer du texte
- Éviter les visages identifiables
```

---

## VARIABLES REQUISES (Make.com)

| Variable | Type | Exemple | Source |
|----------|------|---------|--------|
| `{{DOMAINE}}` | String | "Français" | Google Sheets - Colonne "Domaine" |
| `{{THEME}}` | String | "Identifier le groupe sujet" | Google Sheets - Colonne "Thème" |

---

## EXEMPLE DE SORTIE ATTENDUE

```json
{
  "prompts": [
    "classe de CM1 en Guyane, tableau vert, lumière naturelle venant de grandes fenêtres, carte de la Guyane affichée au mur, angle large, fond neutre",
    "plage de Rémire-Montjoly au matin, horizon doux, ciel léger avec quelques nuages, sable clair, zone centrale claire pour texte",
    "forêt amazonienne claire, feuillage vert doux, profondeur de champ, bokeh naturel, contraste modéré, luminosité filtrée",
    "marché de Cayenne, étals colorés de fruits tropicaux légèrement floutés, bokeh, zone claire au centre pour texte",
    "salle de lecture scolaire en Guyane, étagères en bois, livres colorés, lumière chaude, ambiance sobre et professionnelle",
    "ardoises et cahiers d'écoliers alignés sur table en bois clair, vue oblique, arrière-plan flou, tons neutres et lumineux",
    "plan rapproché de jetons colorés et cubes de manipulation mathématique, fond bois clair, lumière douce, espace central dégagé",
    "carte simplifiée de la Guyane en arrière-plan, tons pastels beige et vert, très discret, centre clair pour texte"
  ]
}
```

---

## INTÉGRATION DANS MAKE.COM

### Option 1 : DALL·E (OpenAI)

**Module** : OpenAI > Create Image

**Configuration** :
- **Prompt** : `{{prompts[X]}}` (extrait du JSON)
- **Size** : 1792x1024 (ratio 16:9 pour slides)
- **Quality** : standard (ou hd pour meilleure qualité)
- **Style** : natural

**Sortie** : URL de l'image générée

### Option 2 : Unsplash API

**Module** : HTTP > Make a request

**Configuration** :
- **URL** : `https://api.unsplash.com/search/photos`
- **Method** : GET
- **Query** :
  - `query` : `{{prompts[X]}}`
  - `orientation` : landscape
  - `per_page` : 1
- **Headers** :
  - `Authorization` : `Client-ID VOTRE_CLE_UNSPLASH`

**Sortie** : URL de l'image (champ `urls.regular`)

### Option 3 : Pexels API

**Module** : HTTP > Make a request

**Configuration** :
- **URL** : `https://api.pexels.com/v1/search`
- **Method** : GET
- **Query** :
  - `query` : `{{prompts[X]}}`
  - `orientation` : landscape
  - `per_page` : 1
- **Headers** :
  - `Authorization` : `VOTRE_CLE_PEXELS`

**Sortie** : URL de l'image (champ `photos[0].src.large`)

---

## FLUX MAKE RECOMMANDÉ

```
┌─────────────────────────┐
│ 1. Appel OpenAI         │
│ (génère 8 prompts JSON) │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ 2. Parse JSON           │
│ (extraire array prompts)│
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ 3. Iterator             │
│ (boucle sur 8 prompts)  │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ 4. DALL·E ou Unsplash   │
│ (générer 1 image)       │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ 5. Google Slides API    │
│ (définir image bg slide)│
└─────────────────────────┘
```

---

## CHECKLIST QUALITÉ (à intégrer dans Make)

- ✅ 8 prompts générés (1 par slide)
- ✅ Tous les prompts sont contextualisés Guyane ou scolaire
- ✅ Aucun prompt ne contient "neige", "pommes", "Eiffel", etc.
- ✅ Tous les prompts prévoient un espace clair pour texte
- ✅ Aucun prompt ne demande de texte dans l'image
- ✅ Images générées en format 16:9 (1792x1024 ou équivalent)

---

## PROMPTS GÉNÉRIQUES PAR DOMAINE (fallback)

Si la génération échoue ou pour accélérer, voici des prompts génériques réutilisables :

| Domaine | Prompt générique |
|---------|------------------|
| Français | "tableau noir avec phrase écrite à la craie, classe en Guyane, lumière naturelle, fond sobre" |
| Maths | "ardoises et jetons de calcul sur table en bois, lumière douce, fond neutre, zone centrale claire" |
| Sciences | "feuilles de plantes tropicales, lumière filtrée, bokeh naturel, tons verts et lumineux" |
| Anglais | "drapeaux anglophones discrets en arrière-plan, fond neutre beige, ambiance internationale sobre" |
| EMC | "cercle de chaises vide dans classe, lumière chaude, ambiance bienveillante et collaborative" |
| Géographie | "carte de la Guyane simplifiée, tons pastels, fond clair, très discret" |
| Histoire | "vieux livre ouvert, lumière douce, fond bois, ambiance studieuse" |

---

## NOTES IMPORTANTES

1. **Respect RGPD** : ne jamais demander de visages d'enfants identifiables
2. **Accessibilité** : contraste suffisant pour lecture de texte (WCAG AA minimum)
3. **Cohérence visuelle** : utiliser des tonalités similaires sur les 8 slides
4. **Performance** : privilégier Unsplash/Pexels (gratuit, rapide) vs DALL·E (payant, lent)
5. **Cache** : stocker les images générées dans Drive pour réutilisation
