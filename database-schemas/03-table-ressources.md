# Table : Ressources (Banque pédagogique)

**Nom de l'onglet** : `Ressources`

**Description** : Banque centralisée de toutes les ressources pédagogiques (dictées, fiches de manipulation, exercices, documents élèves) avec liens Drive.

---

## STRUCTURE DES COLONNES

| Colonne | Type | Obligatoire | Valeurs possibles | Description | Exemple |
|---------|------|-------------|-------------------|-------------|---------|
| **A - ID_Ressource** | Texte | ✅ | Format: `{DOMAINE}_{TYPE}_{NUM}` | Identifiant unique | `FR_DICT_024` |
| **B - Domaine** | Texte | ✅ | Français, Maths, Sciences, EMC, Anglais | Domaine scolaire | `Français` |
| **C - Type** | Texte | ✅ | Voir liste ci-dessous | Type de ressource | `Dictée` |
| **D - Titre** | Texte | ✅ | Texte libre | Titre descriptif | `Dictée P2S4 – Le marché de Cayenne` |
| **E - Description** | Texte | ❌ | Texte libre | Description courte | `Mots invariables + imparfait` |
| **F - Lien_Drive** | URL | ✅ | URL Google Drive | Lien vers le fichier | `https://drive.google.com/file/d/...` |
| **G - Niveau** | Texte | ✅ | Débutant, Intermédiaire, Avancé, Tous | Niveau de difficulté | `Intermédiaire` |
| **H - Groupe_Cible** | Texte | ❌ | Nom de groupe ou "Tous" | Groupe concerné | `Aïmara` ou `Tous` |
| **I - Periode** | Texte | ❌ | P1, P2, P3, P4, P5 | Période d'utilisation | `P2` |
| **J - Semaine** | Nombre | ❌ | 1-7 | Semaine d'utilisation | `4` |
| **K - Contexte_Guyane** | Checkbox | ✅ | ☐ / ☑ | Contenu contextualisé Guyane | `☑` |
| **L - Date_Ajout** | Date | ✅ | Auto | Date d'ajout de la ressource | `10/11/2024` |
| **M - Auteur** | Texte | ❌ | Texte libre | Créateur de la ressource | `Enseignant CM1` |
| **N - Tags** | Texte | ❌ | Mots-clés séparés par virgules | Pour recherche | `marché,ville,vie quotidienne` |
| **O - Actif** | Checkbox | ✅ | ☐ / ☑ | Ressource active et utilisable | `☑` |

---

## TYPES DE RESSOURCES

### Français
- `Dictée`
- `Lecture`
- `Grammaire`
- `Conjugaison`
- `Orthographe`
- `Vocabulaire`
- `Production écrite`

### Mathématiques
- `Calcul mental`
- `Numération`
- `Géométrie`
- `Mesures`
- `Problèmes`
- `Manipulation`

### Sciences
- `Document élève`
- `Expérience`
- `Observation`
- `Trace écrite`

### Transversal
- `Évaluation`
- `Affichage`
- `Jeu pédagogique`

---

## DONNÉES EXEMPLE

```csv
ID_Ressource,Domaine,Type,Titre,Description,Lien_Drive,Niveau,Groupe_Cible,Periode,Semaine,Contexte_Guyane,Date_Ajout,Auteur,Tags,Actif
FR_DICT_024,Français,Dictée,Dictée P2S4 – Le marché de Cayenne,Mots invariables + imparfait,https://drive.google.com/file/d/xxx,Intermédiaire,Tous,P2,4,☑,10/11/2024,Enseignant CM1,"marché,ville,imparfait",☑
MATH_CALC_012,Maths,Calcul mental,Compléments à 10 – jetons,Manipulation avec jetons colorés,https://drive.google.com/file/d/yyy,Débutant,Fromager,P2,4,☑,10/11/2024,Enseignant CM1,"calcul,addition,manipulation",☑
SCI_DOC_008,Sciences,Document élève,Observer le wapa,Fiche d'observation de l'arbre wapa,https://drive.google.com/file/d/zzz,Tous,Tous,P2,4,☑,10/11/2024,Enseignant CM1,"arbre,forêt,observation",☑
FR_GRAM_015,Français,Grammaire,Le groupe sujet – exercices Aïmara,Phrases courtes avec sujets simples,https://drive.google.com/file/d/aaa,Débutant,Aïmara,P2,4,☑,10/11/2024,Enseignant CM1,"sujet,phrase,grammaire",☑
FR_GRAM_016,Français,Grammaire,Le groupe sujet – exercices Angélique,Phrases moyennes avec GN sujets,https://drive.google.com/file/d/bbb,Intermédiaire,Angélique,P2,4,☑,10/11/2024,Enseignant CM1,"sujet,phrase,grammaire",☑
FR_GRAM_017,Français,Grammaire,Le groupe sujet – exercices Sablier,Phrases complexes avec inversions,https://drive.google.com/file/d/ccc,Avancé,Sablier,P2,4,☑,10/11/2024,Enseignant CM1,"sujet,phrase,grammaire",☑
```

---

## FORMULES GOOGLE SHEETS

### ID auto-généré (si vide)
```
=IF(A2="";"";UPPER(LEFT(B2;2)) & "_" & UPPER(LEFT(C2;4)) & "_" & TEXT(ROW()-1;"000"))
```

### Date d'ajout automatique
```
=IF(L2="";"";NOW())
```

### Compter ressources par domaine
```
=COUNTIF(B:B;"Français")
```

---

## VALIDATION DES DONNÉES

**Colonne B (Domaine)** :
- Type : Liste
- Source : `Français,Maths,Sciences,Anglais,EMC,Géographie,Histoire`

**Colonne C (Type)** :
- Type : Liste
- Source : `Dictée,Lecture,Grammaire,Calcul mental,Problèmes,Document élève,Évaluation`

**Colonne G (Niveau)** :
- Type : Liste
- Source : `Débutant,Intermédiaire,Avancé,Tous`

**Colonne I (Periode)** :
- Type : Liste
- Source : `P1,P2,P3,P4,P5`

---

## EXPORT JSON POUR MAKE.COM

**Format attendu** :
```json
[
  {
    "domaine": "Français",
    "type": "Dictée",
    "titre": "Dictée P2S4 – Le marché de Cayenne",
    "lien": "https://drive.google.com/file/d/xxx",
    "niveau": "Intermédiaire",
    "groupe": "Tous"
  },
  {
    "domaine": "Maths",
    "type": "Manipulation",
    "titre": "Compléments à 10 – jetons",
    "lien": "https://drive.google.com/file/d/yyy",
    "niveau": "Débutant",
    "groupe": "Fromager"
  }
]
```

**Module Make** : Google Sheets > Search Rows

**Configuration** :
```json
{
  "spreadsheet_id": "{{SPREADSHEET_ID}}",
  "sheet_name": "Ressources",
  "filter": [
    {
      "field": "Periode",
      "operator": "equal",
      "value": "{{PERIODE}}"
    },
    {
      "field": "Semaine",
      "operator": "equal",
      "value": "{{SEMAINE}}"
    },
    {
      "field": "Actif",
      "operator": "equal",
      "value": true
    }
  ]
}
```

---

## SCRIPT APPS SCRIPT (recherche par tags)

```javascript
function rechercherParTag(tag) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Ressources');
  var data = sheet.getDataRange().getValues();
  var resultats = [];

  for (var i = 1; i < data.length; i++) {
    var tags = data[i][13]; // Colonne N (Tags)
    if (tags.toLowerCase().includes(tag.toLowerCase())) {
      resultats.push({
        'titre': data[i][3],
        'domaine': data[i][1],
        'lien': data[i][5]
      });
    }
  }

  return resultats;
}
```

---

## INTÉGRATION PHOTOCOPIES

Lors de la génération automatique, Make filtre les ressources pour la semaine en cours et génère automatiquement :

**Table de photocopies** :
| Titre | Groupe | Quantité | Lien Drive |
|-------|--------|----------|------------|
| {{Titre}} | {{Groupe_Cible}} | {{Effectif_Groupe}} | {{Lien_Drive}} |

**Calcul de quantité** :
- Si `Groupe_Cible = "Tous"` → `Quantité = Effectif classe`
- Sinon → `Quantité = Effectif du groupe` (lookup dans table Groupes)

---

## AJOUT RAPIDE DE RESSOURCES

**Formulaire Google Forms** (optionnel)

**Champs** :
1. Domaine (liste)
2. Type (liste)
3. Titre (texte court)
4. Description (paragraphe)
5. Lien Drive (URL)
6. Niveau (liste)
7. Contextualisé Guyane ? (oui/non)

**Action** :
- Réponses → Automatiquement ajoutées à la table Ressources
- Colonne "Actif" = FALSE par défaut (validation manuelle)

---

## AFFICHAGE CONDITIONNEL (Mise en forme)

### Règle 1 : Contexte Guyane ✅
- **Condition** : `K2 = TRUE`
- **Format** : Fond vert clair `#D5F4E6`

### Règle 2 : Contexte Guyane ❌
- **Condition** : `K2 = FALSE`
- **Format** : Fond orange clair `#FCF3CF`

### Règle 3 : Ressource inactive
- **Condition** : `O2 = FALSE`
- **Format** : Texte gris `#95A5A6`, barré

---

## VUES FILTRÉES RECOMMANDÉES

### Vue 1 : Ressources Français
- Filtre : `Domaine = "Français"` ET `Actif = TRUE`
- Tri : `Date_Ajout` descendant

### Vue 2 : Ressources période actuelle
- Filtre : `Periode = "P2"` ET `Actif = TRUE`
- Tri : `Semaine` ascendant

### Vue 3 : Ressources contextualisées Guyane
- Filtre : `Contexte_Guyane = TRUE` ET `Actif = TRUE`
- Tri : `Domaine`, puis `Type`

---

## CHECKLIST AVANT UTILISATION

- ✅ Toutes les ressources ont un lien Drive valide
- ✅ Les liens sont accessibles (permissions configurées)
- ✅ Les ressources sont contextualisées Guyane (si cochée)
- ✅ Les types correspondent aux domaines
- ✅ Les groupes cibles existent dans la table Groupes
- ✅ Les ID sont uniques

---

## MAINTENANCE

**Nettoyage périodique** (fin de période) :
1. Désactiver les ressources obsolètes (`Actif = FALSE`)
2. Archiver les ressources anciennes (déplacer vers onglet "Archive")
3. Vérifier les liens Drive cassés
4. Mettre à jour les tags pour améliorer la recherche

---

**Table créée pour le système CM1 MOUTOUCHI**
*Version 1.0 - Compatible Make.com*
