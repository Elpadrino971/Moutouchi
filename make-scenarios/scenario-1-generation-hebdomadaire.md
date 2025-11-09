# Scénario Make.com n°1 : Génération hebdomadaire automatique

**Nom du scénario** : `CM1_MOUTOUCHI_Generation_Hebdo`

**Déclencheur** : Jeudi 18h00 (chaque semaine)

**Objectif** : Générer automatiquement le cahier journal, le PowerPoint, la feuille de photocopies et envoyer le message WhatsApp récapitulatif.

---

## ARCHITECTURE GLOBALE

```
┌─────────────────────────────────────────────────────────────────┐
│                    SCÉNARIO 1 - GÉNÉRATION HEBDO                │
└─────────────────────────────────────────────────────────────────┘

1️⃣  [Scheduler]           → Jeudi 18h00
        ↓
2️⃣  [Google Sheets]       → Lire semaine active (Statut = "À préparer")
        ↓
3️⃣  [Router - Condition]  → Si semaine trouvée ?
        ↓ OUI
4️⃣  [Google Sheets]       → Lire groupes actifs
        ↓
5️⃣  [Google Sheets]       → Lire ressources semaine
        ↓
6️⃣  [Tools - JSON]        → Construire GROUPS_JSON
        ↓
7️⃣  [Tools - JSON]        → Construire RESSOURCES_JSON
        ↓
8️⃣  [OpenAI - GPT-4]      → Générer cahier journal (Prompt 1)
        ↓
9️⃣  [Google Docs]         → Créer document Word
        ↓
🔟  [OpenAI - GPT-4]      → Générer contenu slides (Prompt 2)
        ↓
1️⃣1️⃣ [OpenAI - DALL·E]     → Générer 8 images de fond (Prompt 3)
        ↓
1️⃣2️⃣ [Google Slides]      → Créer PowerPoint + insérer contenu + images
        ↓
1️⃣3️⃣ [Google Sheets]      → Créer feuille Photocopies
        ↓
1️⃣4️⃣ [Iterator]           → Pour chaque ressource → ajouter ligne photocopies
        ↓
1️⃣5️⃣ [Google Drive]       → Déplacer fichiers dans dossier Période/Semaine
        ↓
1️⃣6️⃣ [Google Sheets]      → Mettre à jour table Semaines (liens + statut)
        ↓
1️⃣7️⃣ [WhatsApp - Twilio]  → Envoyer message récapitulatif
        ↓
1️⃣8️⃣ [FIN]
```

---

## MODULES DÉTAILLÉS

### 1️⃣ Module : Scheduler (Déclencheur)

**Type** : `Scheduled trigger`

**Configuration** :
- **Schedule** : `Custom`
- **Day of week** : Thursday (Jeudi)
- **Hour** : 18
- **Minute** : 00
- **Timezone** : Europe/Paris (ou America/Cayenne pour Guyane)

**Output** : Timestamp

---

### 2️⃣ Module : Google Sheets - Search Rows

**Type** : `Google Sheets > Search Rows`

**Configuration** :
- **Spreadsheet** : ID de votre Google Sheets principal
- **Sheet** : `Semaines`
- **Filter** :
  ```
  Column: Statut
  Condition: Text operators > Equal to
  Value: À préparer
  ```
- **Max results** : 1
- **Sort order** : Date_Debut (ascending)

**Output** :
```json
{
  "id": "P2S4",
  "periode": "P2",
  "semaine": 4,
  "date_debut": "27/11/2024",
  "domaine": "Français",
  "theme": "Identifier le groupe sujet",
  "duree": 45
}
```

---

### 3️⃣ Module : Router (Condition)

**Type** : `Flow control > Router`

**Route 1** : "Semaine trouvée"
- **Condition** : `{{2.id}}` is not empty
- **Action** : Continuer

**Route 2** : "Aucune semaine"
- **Condition** : `{{2.id}}` is empty
- **Action** : Stop + Send email notification (optionnel)

---

### 4️⃣ Module : Google Sheets - Search Rows (Groupes)

**Type** : `Google Sheets > Search Rows`

**Configuration** :
- **Spreadsheet** : Même ID
- **Sheet** : `Groupes`
- **Filter** :
  ```
  Column: Domaine
  Condition: Text operators > Equal to
  Value: {{2.domaine}}

  AND

  Column: Actif
  Condition: Boolean > Equal to
  Value: true
  ```
- **Max results** : 10

**Output** :
```json
[
  {"nom_groupe": "Aïmara", "niveau": "Débutant", "effectif": 7},
  {"nom_groupe": "Angélique", "niveau": "Intermédiaire", "effectif": 10},
  {"nom_groupe": "Sablier", "niveau": "Avancé", "effectif": 8}
]
```

---

### 5️⃣ Module : Google Sheets - Search Rows (Ressources)

**Type** : `Google Sheets > Search Rows`

**Configuration** :
- **Spreadsheet** : Même ID
- **Sheet** : `Ressources`
- **Filter** :
  ```
  Column: Periode
  Condition: Equal to
  Value: {{2.periode}}

  AND

  Column: Semaine
  Condition: Equal to
  Value: {{2.semaine}}

  AND

  Column: Actif
  Condition: Equal to
  Value: true
  ```

**Output** :
```json
[
  {
    "domaine": "Français",
    "type": "Dictée",
    "titre": "Dictée P2S4",
    "lien": "https://drive.google.com/...",
    "groupe": "Tous"
  }
]
```

---

### 6️⃣ Module : Tools - Create JSON (Groupes)

**Type** : `Tools > Create JSON`

**Configuration** :
- **JSON structure** :
  ```json
  {
    "{{lower(2.domaine)}}": [
      {{map(4.array; "nom_groupe")}}
    ]
  }
  ```

**Exemple de sortie** :
```json
{
  "français": ["Aïmara", "Angélique", "Sablier"]
}
```

---

### 7️⃣ Module : Tools - Create JSON (Ressources)

**Type** : `Tools > Create JSON`

**Configuration** :
- **JSON structure** :
  ```json
  [
    {{map(5.array; '{"domaine":"' + domaine + '","type":"' + type + '","titre":"' + titre + '","lien":"' + lien_drive + '"}')}}
  ]
  ```

**Exemple de sortie** :
```json
[
  {"domaine":"Français","type":"Dictée","titre":"Dictée P2S4","lien":"..."}
]
```

---

### 8️⃣ Module : OpenAI - Create a Completion (Cahier Journal)

**Type** : `OpenAI > Create a Completion`

**Configuration** :
- **Model** : `gpt-4` ou `gpt-4o`
- **Messages** :

**System message** :
```
Tu es un concepteur pédagogique CM1. Tu produis un document clair, exploitable, sans remplissage, aligné sur les programmes officiels (Cycle 3), ancré en Guyane (contextes, exemples, images mentales locales).

Exigences clés :
- Démarrer par une QUESTION-PROBLÈME (réflexion des élèves avant le cours).
- Méthodologie explicite et répétée : "Observer → Questionner → Vérifier" (+ variantes selon la notion).
- Différenciation dynamique par groupes (noms d'arbres/endémiques fournis).
- Intégrer systématiquement : manipulations, rôles de tuteurs, rituels d'autonomie (tenue de cahier, dictée, résolution de problème).
- Ton neutre, direct, professionnel. Pas de clichés européens/US.
- Phrases, lieux, objets, faune/flore = Guyane (ex. Cayenne, Rémire, criques, wapa, couac, manioc, colibris...).
- Pas d'images : seulement texte structuré.
- Sortie MARKDOWN stricte, sections balisées.
```

**User message** :
```
Contexte semaine :
- Période : {{2.periode}}
- Semaine : {{2.semaine}}
- Domaine : {{2.domaine}}
- Thème / Notion : {{2.theme}}
- Durée : {{2.duree}} minutes
- Emploi du temps : Lundi–Jeudi, 8h–11h30 et 13h20–16h

Groupes & différenciation (JSON) :
{{6.json}}

Ressources disponibles (liens Drive + type) :
{{7.json}}

Contraintes :
- Démarrer par une question-problème contextualisée Guyane.
- Intégrer une manipulation concrète (matériel accessible : ardoises, jetons, cubes, balances, bandes-phrases).
- Décrire précisément les rôles : enseignant, tuteurs, élèves.
- Différencier par groupe (niveaux/profils) en NAMING local fourni ci-dessus.
- Rappeler en fin de séance : rituels d'autonomie (tenue de cahier / dictée / résolution de problème).
- Ajouter un encadré "Photocopies à prévoir" relié aux liens fournis.

[VOIR FORMAT COMPLET DANS prompts/01-cahier-journal-prompt.md]

Produis UNIQUEMENT le markdown de la séance demandée. Pas d'explications hors structure.
```

**Output** : Texte markdown complet du cahier journal

---

### 9️⃣ Module : Google Docs - Create a Document from Text

**Type** : `Google Docs > Create a Document from Text`

**Configuration** :
- **Document name** : `Cahier_Journal_{{2.periode}}_{{2.semaine}}_{{2.domaine}}`
- **Document content** : `{{8.text}}`
- **Folder** : ID du dossier Drive temporaire

**Output** :
```json
{
  "document_id": "xxx",
  "document_url": "https://docs.google.com/document/d/xxx"
}
```

---

### 🔟 Module : OpenAI - Create a Completion (Slides JSON)

**Type** : `OpenAI > Create a Completion`

**Configuration** :
- **Model** : `gpt-4` ou `gpt-4o`
- **Messages** :

**System message** :
```
Tu génères le contenu exact de 8 diapositives pédagogiques CM1, centrées réflexion/méthodo, ancrées en Guyane, sans jargon ni remplissage.

Toujours commencer par une question-problème.

Retourne du JSON strict, clés figées, pas de texte hors JSON.
```

**User message** :
```
Variables :
- Domaine : {{2.domaine}}
- Thème : {{2.theme}}
- Période/Semaine : {{2.periode}}/{{2.semaine}}
- Groupes : {{6.json}}
- Contrainte : images/fonds = contexte Guyane (libres de droit ou IA)

Retourne un JSON avec EXACTEMENT ces clés :
[VOIR FORMAT COMPLET DANS prompts/02-slides-prompt.md]
```

**Response format** : JSON

**Output** :
```json
{
  "slide1": {...},
  "slide2": {...},
  ...
}
```

---

### 1️⃣1️⃣ Module : OpenAI - Create Image (DALL·E)

**Type** : `OpenAI > Create Image`

**Configuration** :
- **Model** : `dall-e-3`
- **Prompt** : `{{10.slide1.bg_prompt}}`
- **Size** : `1792x1024` (16:9)
- **Quality** : `standard`
- **Number** : 1

**Note** : Répéter ce module 8 fois (ou utiliser un Iterator) pour générer les 8 images

**Output** : URL de l'image

---

### 1️⃣2️⃣ Module : Google Slides - Create Presentation

**Type** : `Google Slides > Create Presentation`

**Configuration** :
- **Presentation name** : `CM1_{{2.periode}}_{{2.semaine}}_{{2.domaine}}`
- **Folder** : ID du dossier temporaire

**Puis** : Utiliser `Google Slides > Make an API Call` pour :
1. Créer 8 slides
2. Remplir le contenu (titres, textes, listes)
3. Insérer les images de fond

**Output** :
```json
{
  "presentation_id": "yyy",
  "presentation_url": "https://docs.google.com/presentation/d/yyy"
}
```

---

### 1️⃣3️⃣ Module : Google Sheets - Add a Row (Photocopies)

**Type** : `Google Sheets > Add Multiple Rows`

**Configuration** :
- **Spreadsheet** : Même ID
- **Sheet** : `Photocopies`
- **Values** : Utiliser Iterator sur les ressources (module 5)

**Colonnes à remplir** :
```
Semaine_ID: {{2.id}}
Domaine: {{5.domaine}}
Titre_Fiche: {{5.titre}}
Lien_Drive: {{5.lien_drive}}
Groupe_Concerne: {{5.groupe_cible}}
Quantite: {{if(5.groupe_cible = "Tous"; 25; lookup_effectif)}}
Type_Document: A4 N&B
Priorite: Normale
Imprime: false
```

---

### 1️⃣4️⃣ Module : Iterator (Ressources → Photocopies)

**Type** : `Flow control > Iterator`

**Input** : `{{5.array}}` (ressources)

**Action** : Pour chaque ressource, ajouter une ligne (module 13)

---

### 1️⃣5️⃣ Module : Google Drive - Move a File

**Type** : `Google Drive > Move a File` (x2)

**Configuration 1** : Déplacer le cahier journal
- **File ID** : `{{9.document_id}}`
- **Target folder** : `/CM1_MOUTOUCHI/Periode_{{2.periode}}/Semaine_{{2.semaine}}/`

**Configuration 2** : Déplacer le PowerPoint
- **File ID** : `{{12.presentation_id}}`
- **Target folder** : Même dossier

---

### 1️⃣6️⃣ Module : Google Sheets - Update a Row

**Type** : `Google Sheets > Update a Row`

**Configuration** :
- **Spreadsheet** : Même ID
- **Sheet** : `Semaines`
- **Row number** : `{{2.__row_number}}`
- **Values** :
  ```
  Statut: Générée
  Generee_Le: {{now}}
  Lien_Cahier_Journal: {{9.document_url}}
  Lien_PowerPoint: {{12.presentation_url}}
  Lien_Photocopies: {{LIEN_FEUILLE_PHOTOCOPIES}}
  ```

---

### 1️⃣7️⃣ Module : WhatsApp - Send a Message (Twilio)

**Type** : `Twilio > Send a WhatsApp Message`

**Configuration** :
- **From** : `whatsapp:+14155238886` (numéro Twilio)
- **To** : `whatsapp:+594XXXXXXXXX` (votre numéro)
- **Body** :
  ```
  🌿 CM1 MOUTOUCHI – {{2.periode}} {{2.semaine}}

  📘 Cahier journal : prêt ✅
  🎞️ Diaporama : prêt ✅
  📄 Photocopies : à imprimer vendredi (avant 16h)

  📎 Dossier complet : {{LIEN_DOSSIER}}

  🔔 Rappel automatique demain à 7h30 !
  ```

**Alternative** : WhatsApp Cloud API (Meta)

---

## VARIABLES GLOBALES

**À configurer dans Make** :
- `SPREADSHEET_ID` : ID de votre Google Sheets principal
- `DRIVE_FOLDER_ROOT` : ID du dossier racine Drive
- `WHATSAPP_NUMBER` : Votre numéro WhatsApp
- `OPENAI_API_KEY` : Clé API OpenAI (gpt-4 + dall-e-3)
- `TWILIO_ACCOUNT_SID` : Compte Twilio
- `TWILIO_AUTH_TOKEN` : Token Twilio

---

## GESTION DES ERREURS

### Error handler (global)

**En cas d'erreur** :
1. Logger l'erreur dans Google Sheets (onglet "Logs")
2. Envoyer un email à l'enseignant
3. Ne PAS changer le statut de la semaine (reste "À préparer")

**Module** : `Tools > Set Variable`
- **Variable name** : `error_message`
- **Value** : `{{exception.message}}`

**Puis** : `Google Sheets > Add a Row` (onglet "Logs")
- Date, Scénario, Erreur, Module

---

## OPTIMISATIONS

1. **Cache GPT** : Stocker les réponses IA pour éviter les régénérations
2. **Parallélisation** : Générer cahier journal et slides en parallèle
3. **Batch images** : Générer les 8 images DALL·E en une seule fois (si API le permet)
4. **Compression** : Compresser les images avant insertion dans Slides

---

## TESTS RECOMMANDÉS

### Test 1 : Génération complète
- Créer une semaine fictive "TEST_P0S0"
- Lancer manuellement le scénario
- Vérifier tous les fichiers générés

### Test 2 : Aucune semaine à préparer
- Vérifier que le scénario s'arrête proprement
- Pas d'email d'erreur

### Test 3 : Erreur API OpenAI
- Simuler une erreur (quota dépassé)
- Vérifier que l'erreur est loggée
- Vérifier que le statut reste "À préparer"

---

## DÉPLOIEMENT

1. Importer le blueprint JSON (fourni séparément)
2. Configurer les connexions (Google, OpenAI, Twilio)
3. Tester avec une semaine fictive
4. Activer le scheduler
5. Surveiller les premiers lancemen ts automatiques

---

**Scénario créé pour le système CM1 MOUTOUCHI**
*Version 1.0 - Prêt pour Make.com*
