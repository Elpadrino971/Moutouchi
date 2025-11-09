# Table : Semaines (Planning)

**Nom de l'onglet** : `Semaines`

**Description** : Table principale qui définit le planning hebdomadaire et déclenche la génération automatique.

---

## STRUCTURE DES COLONNES

| Colonne | Type | Obligatoire | Valeurs possibles | Description | Exemple |
|---------|------|-------------|-------------------|-------------|---------|
| **A - ID** | Texte | ✅ | Format: `P{X}S{Y}` | Identifiant unique période + semaine | `P2S4` |
| **B - Période** | Texte | ✅ | P1, P2, P3, P4, P5 | Période scolaire | `P2` |
| **C - Semaine** | Nombre | ✅ | 1-7 | Numéro de semaine dans la période | `4` |
| **D - Date_Debut** | Date | ✅ | Format: JJ/MM/AAAA | Premier jour de la semaine (lundi) | `13/11/2024` |
| **E - Date_Fin** | Date | ✅ | Format: JJ/MM/AAAA | Dernier jour de la semaine (jeudi) | `16/11/2024` |
| **F - Domaine_Principal** | Texte | ✅ | Français, Maths, Sciences, EMC, Anglais | Domaine de la séance principale | `Français` |
| **G - Theme** | Texte | ✅ | Texte libre | Thème/notion à enseigner | `Identifier le groupe sujet` |
| **H - Duree** | Nombre | ✅ | 30-60 (minutes) | Durée de la séance en minutes | `45` |
| **I - Statut** | Liste | ✅ | `À préparer`, `En cours`, `Générée`, `Terminée` | État d'avancement | `À préparer` |
| **J - Generee_Le** | DateTime | ❌ | Auto | Date/heure de génération automatique | `14/11/2024 18:00` |
| **K - Lien_Cahier_Journal** | URL | ❌ | Auto | Lien vers le document Word/Docs généré | `https://docs.google.com/...` |
| **L - Lien_PowerPoint** | URL | ❌ | Auto | Lien vers le PowerPoint/Slides généré | `https://docs.google.com/...` |
| **M - Lien_Photocopies** | URL | ❌ | Auto | Lien vers la feuille de photocopies | `https://docs.google.com/...` |
| **N - WhatsApp_Envoye** | Checkbox | ❌ | ☐ / ☑ | Message WhatsApp envoyé | `☑` |
| **O - Remarques** | Texte | ❌ | Texte libre | Notes de l'enseignant | `Ajouter exemple créole` |

---

## DONNÉES EXEMPLE

```csv
ID,Période,Semaine,Date_Debut,Date_Fin,Domaine_Principal,Theme,Duree,Statut,Generee_Le,Lien_Cahier_Journal,Lien_PowerPoint,Lien_Photocopies,WhatsApp_Envoye,Remarques
P2S1,P2,1,06/11/2024,09/11/2024,Français,Le verbe et son infinitif,45,Terminée,06/11/2024 18:00,https://docs.google.com/document/d/xxx,https://docs.google.com/presentation/d/yyy,https://docs.google.com/spreadsheets/d/zzz,☑,
P2S2,P2,2,13/11/2024,16/11/2024,Maths,La multiplication posée,50,Terminée,13/11/2024 18:00,https://docs.google.com/document/d/xxx,https://docs.google.com/presentation/d/yyy,https://docs.google.com/spreadsheets/d/zzz,☑,
P2S3,P2,3,20/11/2024,23/11/2024,Sciences,Le cycle de l'eau en Guyane,45,Terminée,20/11/2024 18:00,https://docs.google.com/document/d/xxx,https://docs.google.com/presentation/d/yyy,https://docs.google.com/spreadsheets/d/zzz,☑,
P2S4,P2,4,27/11/2024,30/11/2024,Français,Identifier le groupe sujet,45,À préparer,,,,,Contexte: marché de Cayenne
P2S5,P2,5,04/12/2024,07/12/2024,EMC,Le respect des différences,40,À préparer,,,,,
```

---

## FORMULES GOOGLE SHEETS

### Colonne A (ID) - Auto-génération
```
=CONCATENATE("P";B2;"S";C2)
```

### Colonne J (Generee_Le) - Timestamp automatique
```
=IF(I2="Générée";NOW();"")
```

### Validation des données

**Colonne F (Domaine_Principal)** :
- Type : Liste
- Source : `Français,Maths,Sciences,EMC,Anglais,Géographie,Histoire`

**Colonne I (Statut)** :
- Type : Liste
- Source : `À préparer,En cours,Générée,Terminée`

---

## TRIGGERS MAKE.COM

### Déclencheur automatique (Jeudi 18h00)

**Module** : Google Sheets > Search Rows

**Configuration** :
```json
{
  "spreadsheet_id": "{{SPREADSHEET_ID}}",
  "sheet_name": "Semaines",
  "filter": {
    "field": "Statut",
    "operator": "equal",
    "value": "À préparer"
  }
}
```

**Condition de filtrage supplémentaire** :
- La `Date_Debut` doit être dans les 7 prochains jours

**Actions à déclencher** :
1. Générer le cahier journal (prompt 1)
2. Générer le PowerPoint (prompt 2)
3. Générer la feuille de photocopies
4. Uploader les fichiers sur Drive
5. Mettre à jour les colonnes K, L, M avec les liens
6. Changer le statut à "Générée"
7. Envoyer le message WhatsApp
8. Cocher la case N (WhatsApp_Envoye)

---

## DÉCLENCHEUR MANUEL

**Fonctionnalité** : Bouton "Générer maintenant" dans Google Sheets

**Installation** :
1. Apps Script > Nouveau script
2. Code :
```javascript
function genererMaintenant() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var row = sheet.getActiveRange().getRow();

  // Appeler le webhook Make.com
  var webhookUrl = 'https://hook.eu1.make.com/VOTRE_WEBHOOK_ID';

  var options = {
    'method': 'post',
    'contentType': 'application/json',
    'payload': JSON.stringify({
      'row_number': row,
      'trigger': 'manual'
    })
  };

  UrlFetchApp.fetch(webhookUrl, options);

  SpreadsheetApp.getUi().alert('Génération lancée ! Vous recevrez un message WhatsApp dans quelques minutes.');
}
```

3. Ajouter un bouton dans la feuille (Insertion > Dessin > Bouton)
4. Assigner la fonction `genererMaintenant`

---

## VUES FILTRÉES RECOMMANDÉES

### Vue 1 : Semaines à préparer
- Filtre : `Statut = "À préparer"`
- Tri : `Date_Debut` ascendant

### Vue 2 : Semaines générées
- Filtre : `Statut = "Générée"`
- Tri : `Generee_Le` descendant

### Vue 3 : Archive période actuelle
- Filtre : `Période = "P2"` (ajuster selon besoin)
- Tri : `Semaine` ascendant

---

## EXPORT POUR MAKE.COM

**Format attendu par Make** : JSON

**Exemple de sortie** :
```json
{
  "id": "P2S4",
  "periode": "P2",
  "semaine": 4,
  "date_debut": "27/11/2024",
  "date_fin": "30/11/2024",
  "domaine": "Français",
  "theme": "Identifier le groupe sujet",
  "duree": 45,
  "statut": "À préparer",
  "remarques": "Contexte: marché de Cayenne"
}
```

**Module Make** : Google Sheets > Get a Row

**Configuration** :
- Spreadsheet : ID de votre feuille
- Sheet : `Semaines`
- Row number : `{{row_number}}` (détecté automatiquement)

---

## CHECKLIST AVANT UTILISATION

- ✅ Toutes les colonnes sont créées
- ✅ Les validations de données sont configurées
- ✅ Les formules sont appliquées
- ✅ Le bouton "Générer maintenant" fonctionne
- ✅ Les données exemple sont supprimées (ou conservées pour test)
- ✅ Les permissions Drive sont configurées (Make.com a accès en écriture)

---

**Table créée pour le système CM1 MOUTOUCHI**
*Version 1.0 - Compatible Make.com*
