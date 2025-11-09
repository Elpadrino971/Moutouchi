# Table : Photocopies (Gestion impression)

**Nom de l'onglet** : `Photocopies`

**Description** : Table générée automatiquement chaque semaine pour suivre les photocopies à imprimer et leur statut de validation.

---

## STRUCTURE DES COLONNES

| Colonne | Type | Obligatoire | Valeurs possibles | Description | Exemple |
|---------|------|-------------|-------------------|-------------|---------|
| **A - Semaine_ID** | Texte | ✅ | Format: `P{X}S{Y}` | Identifiant semaine | `P2S4` |
| **B - Domaine** | Texte | ✅ | Français, Maths, Sciences, etc. | Domaine scolaire | `Français` |
| **C - Titre_Fiche** | Texte | ✅ | Texte libre | Nom de la ressource | `Dictée P2S4 – Marché de Cayenne` |
| **D - Lien_Drive** | URL | ✅ | URL Google Drive | Lien vers le fichier à imprimer | `https://drive.google.com/...` |
| **E - Groupe_Concerne** | Texte | ✅ | Nom de groupe ou "Tous" | Groupe destinataire | `Aïmara` ou `Tous` |
| **F - Quantite** | Nombre | ✅ | 1-30 | Nombre de copies à imprimer | `25` |
| **G - Type_Document** | Texte | ✅ | A4 couleur, A4 N&B, A3, etc. | Type d'impression | `A4 N&B` |
| **H - Priorite** | Texte | ✅ | Haute, Normale, Basse | Urgence d'impression | `Haute` |
| **I - Imprime** | Checkbox | ✅ | ☐ / ☑ | Statut d'impression | `☐` |
| **J - Date_Impression** | DateTime | ❌ | Auto | Date/heure de validation | `15/11/2024 08:30` |
| **K - Remarques** | Texte | ❌ | Texte libre | Notes enseignant | `Imprimer recto-verso` |

---

## DONNÉES EXEMPLE

```csv
Semaine_ID,Domaine,Titre_Fiche,Lien_Drive,Groupe_Concerne,Quantite,Type_Document,Priorite,Imprime,Date_Impression,Remarques
P2S4,Français,Dictée P2S4 – Marché de Cayenne,https://drive.google.com/file/d/xxx,Tous,25,A4 N&B,Haute,☐,,
P2S4,Maths,Compléments à 10 – jetons,https://drive.google.com/file/d/yyy,Fromager,6,A4 Couleur,Normale,☐,,Plastifier si possible
P2S4,Sciences,Observer le wapa,https://drive.google.com/file/d/zzz,Tous,25,A4 N&B,Normale,☐,,
P2S4,Français,Exercices groupe sujet – Aïmara,https://drive.google.com/file/d/aaa,Aïmara,7,A4 N&B,Haute,☐,,
P2S4,Français,Exercices groupe sujet – Angélique,https://drive.google.com/file/d/bbb,Angélique,10,A4 N&B,Haute,☐,,
P2S4,Français,Exercices groupe sujet – Sablier,https://drive.google.com/file/d/ccc,Sablier,8,A4 N&B,Haute,☐,,
```

---

## GÉNÉRATION AUTOMATIQUE (Make.com)

### Processus

**Déclencheur** : Jeudi 18h00 (après génération des documents)

**Étapes** :
1. **Lire les ressources** de la semaine (table Ressources)
2. **Pour chaque ressource** :
   - Récupérer le groupe cible
   - Lookup effectif du groupe (table Groupes)
   - Calculer la quantité :
     - Si `Groupe = "Tous"` → `Quantité = Effectif classe (25)`
     - Sinon → `Quantité = Effectif du groupe`
3. **Créer une ligne** dans la table Photocopies
4. **Trier** par domaine, puis priorité

**Module Make** : Google Sheets > Add a Row

**Configuration** :
```json
{
  "spreadsheet_id": "{{SPREADSHEET_ID}}",
  "sheet_name": "Photocopies",
  "values": {
    "Semaine_ID": "{{PERIODE}}S{{SEMAINE}}",
    "Domaine": "{{ressource.domaine}}",
    "Titre_Fiche": "{{ressource.titre}}",
    "Lien_Drive": "{{ressource.lien}}",
    "Groupe_Concerne": "{{ressource.groupe}}",
    "Quantite": "{{quantite_calculee}}",
    "Type_Document": "A4 N&B",
    "Priorite": "Normale",
    "Imprime": false
  }
}
```

---

## FORMULES GOOGLE SHEETS

### Total de copies à imprimer
```
=SUM(F:F)
```

### Nombre de fiches imprimées
```
=COUNTIF(I:I;TRUE)
```

### Nombre de fiches restantes
```
=COUNTIF(I:I;FALSE)
```

### Date d'impression automatique
```
=IF(I2=TRUE;NOW();"")
```

### Indicateur visuel
```
=IF(I2=TRUE;"✅ Fait";"⏳ À faire")
```

---

## VALIDATION DES DONNÉES

**Colonne B (Domaine)** :
- Type : Liste
- Source : `Français,Maths,Sciences,Anglais,EMC,Géographie,Histoire`

**Colonne G (Type_Document)** :
- Type : Liste
- Source : `A4 N&B,A4 Couleur,A3 N&B,A3 Couleur`

**Colonne H (Priorite)** :
- Type : Liste
- Source : `Haute,Normale,Basse`

---

## AFFICHAGE CONDITIONNEL (Mise en forme)

### Règle 1 : Priorité Haute
- **Condition** : `H2 = "Haute"`
- **Format** : Fond rouge clair `#FADBD8`, texte rouge foncé `#C0392B`

### Règle 2 : Priorité Normale
- **Condition** : `H2 = "Normale"`
- **Format** : Fond jaune clair `#FCF3CF`

### Règle 3 : Priorité Basse
- **Condition** : `H2 = "Basse"`
- **Format** : Fond gris clair `#ECF0F1`

### Règle 4 : Imprimé ✅
- **Condition** : `I2 = TRUE`
- **Format** : Fond vert clair `#D5F4E6`, texte barré

### Règle 5 : Non imprimé ⏳
- **Condition** : `I2 = FALSE`
- **Format** : Fond blanc, texte normal

---

## MESSAGE WHATSAPP AUTOMATIQUE

### Jeudi 18h00 (après génération)

```
🌿 CM1 MOUTOUCHI – {{PERIODE}} {{SEMAINE}}

📘 Cahier journal : prêt ✅
🎞️ Diaporama : prêt ✅

📄 Photocopies à imprimer (vendredi avant 16h) :

{{#each photocopies}}
• {{Titre_Fiche}} ({{Groupe_Concerne}}) : {{Quantite}} copies
{{/each}}

📊 Total : {{TOTAL_COPIES}} copies

📎 Feuille complète : {{LIEN_FEUILLE_PHOTOCOPIES}}
📁 Dossier Drive : {{LIEN_DOSSIER_SEMAINE}}

🔔 Rappel automatique demain à 7h30 si non validé
```

**Exemple** :
```
🌿 CM1 MOUTOUCHI – P2 S4

📘 Cahier journal : prêt ✅
🎞️ Diaporama : prêt ✅

📄 Photocopies à imprimer (vendredi avant 16h) :

• Dictée P2S4 – Marché de Cayenne (Tous) : 25 copies
• Exercices groupe sujet – Aïmara (Aïmara) : 7 copies
• Exercices groupe sujet – Angélique (Angélique) : 10 copies
• Exercices groupe sujet – Sablier (Sablier) : 8 copies
• Observer le wapa (Tous) : 25 copies

📊 Total : 75 copies

📎 Feuille complète : https://docs.google.com/spreadsheets/d/...
📁 Dossier Drive : https://drive.google.com/drive/folders/...

🔔 Rappel automatique demain à 7h30 si non validé
```

---

### Vendredi 7h30 (rappel si non imprimé)

**Déclencheur Make** : Scheduler + Condition

**Condition** :
```json
{
  "filter": {
    "field": "Imprime",
    "operator": "equal",
    "value": false
  }
}
```

**Message** :
```
⚠️ CM1 MOUTOUCHI – Rappel photocopies

📄 Pense à imprimer les photocopies P{{PERIODE}}S{{SEMAINE}} avant 16h !

📊 Restant : {{NOMBRE_NON_IMPRIME}} fiches ({{TOTAL_COPIES_RESTANT}} copies)

📎 Feuille : {{LIEN_FEUILLE_PHOTOCOPIES}}

Coche les cases une fois imprimé ✅
```

---

## TABLEAU DE BORD VISUEL (optionnel)

**Graphique 1** : Camembert "Statut impression"
- ✅ Imprimé : `COUNTIF(I:I;TRUE)`
- ⏳ À faire : `COUNTIF(I:I;FALSE)`

**Graphique 2** : Barres "Copies par domaine"
- Axe X : Domaines
- Axe Y : `SUMIF(B:B;"Français";F:F)`

**Indicateurs** :
```
━━━━━━━━━━━━━━━━━━━━━━━
📊 PHOTOCOPIES P2S4
━━━━━━━━━━━━━━━━━━━━━━━

Total fiches : 6
Total copies : 75

✅ Imprimé : 0/6
⏳ Restant : 6/6

⚠️ Priorité haute : 4 fiches
━━━━━━━━━━━━━━━━━━━━━━━
```

---

## SCRIPT APPS SCRIPT (validation rapide)

**Fonction** : Cocher toutes les cases d'un coup

```javascript
function toutImprimer() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Photocopies');
  var range = sheet.getRange('I2:I' + sheet.getLastRow());

  var values = [];
  for (var i = 0; i < range.getNumRows(); i++) {
    values.push([true]);
  }

  range.setValues(values);

  SpreadsheetApp.getUi().alert('✅ Toutes les photocopies sont marquées comme imprimées !');
}
```

**Bouton** : Ajouter dans la feuille
- Texte : "✅ Tout imprimer"
- Fonction : `toutImprimer`

---

## ARCHIVAGE

**Fin de semaine** (automatique ou manuel) :
1. Copier les lignes de la semaine
2. Coller dans onglet "Archive_Photocopies"
3. Supprimer les lignes de la semaine en cours
4. Libérer pour la semaine suivante

**Module Make** :
- Déclencheur : Dimanche 20h00
- Action : Move rows (Photocopies → Archive_Photocopies)

---

## CHECKLIST AVANT UTILISATION

- ✅ La table se remplit automatiquement jeudi soir
- ✅ Les quantités sont cohérentes avec les effectifs
- ✅ Les liens Drive sont valides
- ✅ Le message WhatsApp est envoyé
- ✅ Le rappel vendredi fonctionne
- ✅ Les cases se cochent facilement

---

**Table créée pour le système CM1 MOUTOUCHI**
*Version 1.0 - Compatible Make.com*
