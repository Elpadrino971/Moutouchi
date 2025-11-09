# Table : Groupes (Différenciation)

**Nom de l'onglet** : `Groupes`

**Description** : Définit les groupes d'élèves par domaine avec des noms d'arbres/espèces endémiques de Guyane, pour la différenciation pédagogique dynamique.

---

## STRUCTURE DES COLONNES

| Colonne | Type | Obligatoire | Valeurs possibles | Description | Exemple |
|---------|------|-------------|-------------------|-------------|---------|
| **A - Domaine** | Texte | ✅ | Français, Maths, Sciences, Anglais, EMC | Domaine scolaire | `Français` |
| **B - Nom_Groupe** | Texte | ✅ | Noms d'arbres/animaux Guyane | Nom du groupe (contextualisé) | `Aïmara` |
| **C - Niveau** | Texte | ✅ | Débutant, Intermédiaire, Avancé | Niveau du groupe | `Intermédiaire` |
| **D - Effectif** | Nombre | ✅ | 1-30 | Nombre d'élèves dans le groupe | `8` |
| **E - Couleur** | Texte | ❌ | Codes HEX | Couleur pour affichage visuel | `#16A085` |
| **F - Icone** | Emoji | ❌ | Emoji unique | Icône visuelle du groupe | `🌳` |
| **G - Description** | Texte | ❌ | Texte libre | Caractéristiques du groupe | `Élèves à l'aise en lecture` |
| **H - Actif** | Checkbox | ✅ | ☐ / ☑ | Groupe actif cette période | `☑` |

---

## DONNÉES EXEMPLE

```csv
Domaine,Nom_Groupe,Niveau,Effectif,Couleur,Icone,Description,Actif
Français,Aïmara,Débutant,7,#E74C3C,🌺,Besoin de reformulation et de manipulation,☑
Français,Angélique,Intermédiaire,10,#F39C12,🌻,Autonomie croissante,☑
Français,Sablier,Avancé,8,#27AE60,🌿,Très à l'aise - peut tutorer,☑
Maths,Fromager,Débutant,6,#E74C3C,🌳,Calcul mental fragile,☑
Maths,Bois-canon,Intermédiaire,11,#F39C12,🪵,Bonne compréhension des concepts,☑
Maths,Cèdre,Avancé,8,#27AE60,🌲,Raisonnement solide - résolution complexe,☑
Sciences,Wapa,Débutant,7,#E74C3C,🍃,Observation guidée nécessaire,☑
Sciences,Balata,Intermédiaire,10,#F39C12,🌾,Bonne démarche expérimentale,☑
Sciences,Coupi,Avancé,8,#27AE60,🌱,Curiosité scientifique développée,☑
Anglais,Toucan,Débutant,8,#E74C3C,🦜,Prononciation à travailler,☑
Anglais,Ibis,Intermédiaire,9,#F39C12,🦆,Vocabulaire en développement,☑
Anglais,Colibri,Avancé,8,#27AE60,🐦,Aisance orale - peut dialoguer,☑
EMC,Jaguar,Tous,25,#3498DB,🐆,Groupe classe entier,☑
```

---

## NOMS DE GROUPES (Contexte Guyane)

### Arbres et plantes endémiques
- **Aïmara** (arbre tropical)
- **Angélique** (bois précieux)
- **Sablier** (arbre emblématique)
- **Fromager** (arbre géant)
- **Bois-canon** (bois dur)
- **Cèdre** (bois noble)
- **Wapa** (arbre de la forêt)
- **Balata** (arbre à latex)
- **Coupi** (bois résistant)

### Animaux endémiques (alternative)
- **Toucan** (oiseau coloré)
- **Ibis** (oiseau des marais)
- **Colibri** (oiseau rapide)
- **Jaguar** (félin puissant)
- **Caïman** (reptile aquatique)
- **Ara** (perroquet)

---

## FORMULES GOOGLE SHEETS

### Effectif total par domaine
```
=SUMIF(A:A;"Français";D:D)
```

### Nombre de groupes actifs
```
=COUNTIF(H:H;TRUE)
```

---

## VALIDATION DES DONNÉES

**Colonne A (Domaine)** :
- Type : Liste
- Source : `Français,Maths,Sciences,Anglais,EMC,Géographie,Histoire`

**Colonne C (Niveau)** :
- Type : Liste
- Source : `Débutant,Intermédiaire,Avancé,Tous`

---

## EXPORT JSON POUR MAKE.COM

**Format attendu** :
```json
{
  "fr": ["Aïmara", "Angélique", "Sablier"],
  "maths": ["Fromager", "Bois-canon", "Cèdre"],
  "sciences": ["Wapa", "Balata", "Coupi"],
  "anglais": ["Toucan", "Ibis", "Colibri"]
}
```

**Module Make** : Tools > Transform to JSON

**Configuration** :
1. Google Sheets > Search Rows
   - Filter : `Actif = TRUE`
2. Aggregator > Group by `Domaine`
3. Tools > Create JSON
   - Mapping :
     ```
     {
       "{{lower(domaine)}}": ["{{nom_groupe}}"]
     }
     ```

---

## SCRIPT APPS SCRIPT (export automatique)

```javascript
function exportGroupesJSON() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Groupes');
  var data = sheet.getDataRange().getValues();
  var groupes = {};

  for (var i = 1; i < data.length; i++) {
    var domaine = data[i][0].toLowerCase().replace(/é/g,'e');
    var nom = data[i][1];
    var actif = data[i][7];

    if (actif) {
      if (!groupes[domaine]) {
        groupes[domaine] = [];
      }
      groupes[domaine].push(nom);
    }
  }

  return JSON.stringify(groupes);
}
```

---

## AFFICHAGE CONDITIONNEL (Mise en forme)

### Règle 1 : Niveau Débutant
- **Condition** : `C2 = "Débutant"`
- **Format** : Fond rouge clair `#FADBD8`

### Règle 2 : Niveau Intermédiaire
- **Condition** : `C2 = "Intermédiaire"`
- **Format** : Fond orange clair `#FCF3CF`

### Règle 3 : Niveau Avancé
- **Condition** : `C2 = "Avancé"`
- **Format** : Fond vert clair `#D5F4E6`

### Règle 4 : Groupe inactif
- **Condition** : `H2 = FALSE`
- **Format** : Texte gris `#95A5A6`, barré

---

## UTILISATION DANS LES PROMPTS IA

### Prompt cahier journal
```
Groupes & différenciation (JSON) :
{{GROUPS_JSON}}

# Exemple :
# {
#   "français": ["Aïmara","Angélique","Sablier"],
#   ...
# }
```

L'IA utilisera ces noms pour :
1. Créer des activités différenciées par groupe
2. Nommer explicitement les groupes dans le document
3. Calculer les effectifs pour les photocopies

---

## INTERFACE VISUELLE (optionnel)

**Création d'étiquettes de groupes** (PDF à imprimer)

**Module Make** :
1. Google Sheets > Get Rows (Groupes actifs)
2. Iterator (pour chaque groupe)
3. Canva API / Google Slides API
   - Template : Étiquette avec icône + nom + couleur
4. Export PDF
5. Upload Drive `/Étiquettes/`

**Résultat** : Étiquettes imprimables à coller sur les tables

---

## CHECKLIST AVANT UTILISATION

- ✅ Tous les domaines ont au moins 1 groupe
- ✅ Les noms sont contextualisés Guyane (pas de "Groupe A/B/C")
- ✅ Les effectifs sont cohérents avec la classe
- ✅ Les couleurs sont distinctes et accessibles
- ✅ Le script JSON fonctionne
- ✅ Les groupes sont marqués "Actif"

---

**Table créée pour le système CM1 MOUTOUCHI**
*Version 1.0 - Compatible Make.com*
