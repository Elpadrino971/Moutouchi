# Scénario Make.com n°2 : Rappel photocopies

**Nom du scénario** : `CM1_MOUTOUCHI_Rappel_Photocopies`

**Déclencheur** : Vendredi 7h30 (chaque semaine)

**Objectif** : Vérifier si les photocopies ont été imprimées et envoyer un rappel WhatsApp si nécessaire.

---

## ARCHITECTURE GLOBALE

```
┌─────────────────────────────────────────────────────────────────┐
│              SCÉNARIO 2 - RAPPEL PHOTOCOPIES                    │
└─────────────────────────────────────────────────────────────────┘

1️⃣  [Scheduler]           → Vendredi 7h30
        ↓
2️⃣  [Google Sheets]       → Lire table Photocopies (Imprime = FALSE)
        ↓
3️⃣  [Router - Condition]  → Des photocopies non imprimées ?
        ↓ OUI
4️⃣  [Aggregator]          → Compter fiches + total copies
        ↓
5️⃣  [Tools - Text]        → Construire message WhatsApp
        ↓
6️⃣  [WhatsApp - Twilio]   → Envoyer rappel
        ↓
7️⃣  [FIN]

        ↓ NON (route 2)
8️⃣  [FIN - Rien à faire]
```

---

## MODULES DÉTAILLÉS

### 1️⃣ Module : Scheduler (Déclencheur)

**Type** : `Scheduled trigger`

**Configuration** :
- **Schedule** : `Custom`
- **Day of week** : Friday (Vendredi)
- **Hour** : 7
- **Minute** : 30
- **Timezone** : America/Cayenne (Guyane) ou Europe/Paris

**Output** : Timestamp

---

### 2️⃣ Module : Google Sheets - Search Rows

**Type** : `Google Sheets > Search Rows`

**Configuration** :
- **Spreadsheet** : ID de votre Google Sheets principal
- **Sheet** : `Photocopies`
- **Filter** :
  ```
  Column: Imprime
  Condition: Boolean > Equal to
  Value: false
  ```
- **Max results** : 100

**Output** :
```json
[
  {
    "semaine_id": "P2S4",
    "domaine": "Français",
    "titre_fiche": "Dictée P2S4",
    "groupe_concerne": "Tous",
    "quantite": 25,
    "lien_drive": "https://drive.google.com/..."
  },
  {
    "semaine_id": "P2S4",
    "domaine": "Maths",
    "titre_fiche": "Exercices Fromager",
    "groupe_concerne": "Fromager",
    "quantite": 6,
    "lien_drive": "https://drive.google.com/..."
  }
]
```

---

### 3️⃣ Module : Router (Condition)

**Type** : `Flow control > Router`

**Route 1** : "Photocopies non imprimées"
- **Condition** : `{{length(2.array)}}` > 0
- **Action** : Envoyer rappel (modules 4-6)

**Route 2** : "Tout est imprimé"
- **Condition** : `{{length(2.array)}}` = 0
- **Action** : Terminer proprement (optionnel : log success)

---

### 4️⃣ Module : Aggregator (Calculer totaux)

**Type** : `Tools > Numeric aggregator`

**Configuration** :
- **Source module** : Module 2 (Google Sheets)
- **Aggregation function** : Sum
- **Value** : `{{2.quantite}}`

**Output** :
```json
{
  "total_copies": 56,
  "nombre_fiches": 4
}
```

---

### 5️⃣ Module : Tools - Set Variable (Message)

**Type** : `Tools > Set multiple variables`

**Configuration** :

**Variable 1** : `semaine_id`
- **Value** : `{{first(2.array).semaine_id}}`

**Variable 2** : `nombre_fiches`
- **Value** : `{{length(2.array)}}`

**Variable 3** : `total_copies`
- **Value** : `{{4.total}}`

**Variable 4** : `liste_fiches`
- **Value** :
  ```
  {{join(map(2.array; "• " + titre_fiche + " (" + groupe_concerne + ") : " + quantite + " copies"); newline)}}
  ```

**Variable 5** : `message_whatsapp`
- **Value** :
  ```
  ⚠️ CM1 MOUTOUCHI – Rappel photocopies

  📄 Pense à imprimer les photocopies {{5.semaine_id}} avant 16h !

  📊 Restant : {{5.nombre_fiches}} fiches ({{5.total_copies}} copies)

  {{5.liste_fiches}}

  📎 Feuille : {{LIEN_FEUILLE_PHOTOCOPIES}}

  Coche les cases une fois imprimé ✅
  ```

**Output** : Variables prêtes pour WhatsApp

---

### 6️⃣ Module : WhatsApp - Send a Message

**Type** : `Twilio > Send a WhatsApp Message`

**Configuration** :
- **From** : `whatsapp:+14155238886` (Twilio sandbox)
- **To** : `whatsapp:+594XXXXXXXXX` (votre numéro)
- **Body** : `{{5.message_whatsapp}}`

**Alternative** : WhatsApp Cloud API

---

## EXEMPLE DE MESSAGE ENVOYÉ

```
⚠️ CM1 MOUTOUCHI – Rappel photocopies

📄 Pense à imprimer les photocopies P2S4 avant 16h !

📊 Restant : 4 fiches (56 copies)

• Dictée P2S4 – Marché de Cayenne (Tous) : 25 copies
• Exercices Fromager (Fromager) : 6 copies
• Exercices Angélique (Angélique) : 10 copies
• Observer le wapa (Tous) : 25 copies

📎 Feuille : https://docs.google.com/spreadsheets/d/xxx

Coche les cases une fois imprimé ✅
```

---

## VARIANTE : MESSAGE DÉTAILLÉ PAR PRIORITÉ

Si vous voulez un message différent selon la priorité :

### Module 5 (variante) : Router par priorité

**Route 1** : Priorité Haute
- **Condition** : `{{contains(2.array; '"priorite":"Haute"')}}`
- **Message** : `🚨 URGENT : Photocopies priorité HAUTE à imprimer !`

**Route 2** : Priorité Normale
- **Condition** : Autres
- **Message** : `⚠️ Rappel photocopies à imprimer avant 16h`

---

## OPTIMISATION : SECOND RAPPEL (14h)

**Scénario optionnel** : `CM1_MOUTOUCHI_Rappel_Photocopies_14h`

**Déclencheur** : Vendredi 14h00

**Différence** :
- Message plus urgent : `⏰ DERNIER RAPPEL - Plus que 2h !`
- Envoyé seulement si `Imprime = FALSE` encore présent

---

## GESTION DES ERREURS

### Error handler

**En cas d'erreur WhatsApp** :
1. Logger l'erreur dans Google Sheets (onglet "Logs")
2. Envoyer un email de secours
3. Ne PAS bloquer le scénario

**Module** : `Email > Send an Email`
- **To** : Votre email
- **Subject** : `Erreur rappel photocopies CM1`
- **Body** : `Le message WhatsApp n'a pas pu être envoyé. Erreur : {{exception.message}}`

---

## LOGS (optionnel)

**Ajouter un module de log** :

**Type** : `Google Sheets > Add a Row`

**Configuration** :
- **Spreadsheet** : Même ID
- **Sheet** : `Logs`
- **Values** :
  ```
  Date: {{formatDate(now; "DD/MM/YYYY HH:mm")}}
  Scenario: Rappel Photocopies
  Statut: {{if(length(2.array) > 0; "Rappel envoyé"; "Rien à rappeler")}}
  Nombre_Fiches: {{length(2.array)}}
  Total_Copies: {{4.total}}
  ```

---

## VARIABLES GLOBALES

**À configurer dans Make** :
- `SPREADSHEET_ID` : ID de votre Google Sheets principal
- `LIEN_FEUILLE_PHOTOCOPIES` : URL de l'onglet Photocopies
- `WHATSAPP_NUMBER` : Votre numéro WhatsApp
- `TWILIO_ACCOUNT_SID` : Compte Twilio
- `TWILIO_AUTH_TOKEN` : Token Twilio

---

## TESTS RECOMMANDÉS

### Test 1 : Photocopies non imprimées
- Créer des lignes avec `Imprime = FALSE`
- Lancer manuellement le scénario
- Vérifier réception du message WhatsApp

### Test 2 : Tout imprimé
- Toutes les cases `Imprime = TRUE`
- Lancer le scénario
- Vérifier qu'aucun message n'est envoyé

### Test 3 : Erreur WhatsApp
- Utiliser un mauvais numéro
- Vérifier que l'email de secours est envoyé
- Vérifier que l'erreur est loggée

---

## DÉPLOIEMENT

1. Créer le scénario dans Make.com
2. Configurer les connexions (Google Sheets, Twilio)
3. Tester avec des données fictives
4. Activer le scheduler
5. Vérifier le premier vendredi

---

## EXTENSION : NOTIFICATION SI TOUT EST IMPRIMÉ

**Module supplémentaire** (optionnel) :

Si route 2 (tout imprimé), envoyer un message de confirmation :

```
✅ CM1 MOUTOUCHI – Photocopies

Toutes les photocopies P2S4 sont imprimées ! 🎉

Bonne semaine 🌿
```

**Configuration** :
- Même module WhatsApp
- Sur la route 2 du Router
- Message de félicitations

---

**Scénario créé pour le système CM1 MOUTOUCHI**
*Version 1.0 - Prêt pour Make.com*
