# 🚀 Démarrage rapide - CM1 MOUTOUCHI

**Installation express en 4 étapes (30 minutes)**

---

## Avant de commencer

Vous aurez besoin de :
- ✅ Un compte Google (Gmail)
- ✅ Un compte Make.com (gratuit)
- ✅ Une clé API OpenAI (~10€)
- ✅ (Optionnel) Un compte Twilio pour WhatsApp

---

## Étape 1 : Créer la base de données (10 min)

### 1.1 Créer le Google Sheets

1. Aller sur https://sheets.google.com
2. Créer un nouveau fichier : **CM1_MOUTOUCHI_Database**
3. Créer 4 onglets : **Semaines**, **Groupes**, **Ressources**, **Photocopies**

### 1.2 Copier les structures

**Onglet "Semaines"** :
```
ID | Période | Semaine | Date_Debut | Date_Fin | Domaine_Principal | Theme | Duree | Statut
```

**Ajouter une ligne de test** :
```
P2S4 | P2 | 4 | 27/11/2024 | 30/11/2024 | Français | Identifier le groupe sujet | 45 | À préparer
```

**Onglet "Groupes"** :
```
Domaine | Nom_Groupe | Niveau | Effectif | Actif
Français | Aïmara | Débutant | 7 | TRUE
Français | Angélique | Intermédiaire | 10 | TRUE
Français | Sablier | Avancé | 8 | TRUE
```

**Onglet "Ressources"** : (laisser vide pour l'instant)

**Onglet "Photocopies"** : (laisser vide, sera rempli automatiquement)

### 1.3 Noter l'ID du fichier

URL : `https://docs.google.com/spreadsheets/d/[COPIER_CET_ID]/edit`

---

## Étape 2 : Créer la structure Drive (5 min)

1. Créer un dossier : **CM1_MOUTOUCHI**
2. Dedans, créer :
   - `Periode_1/`
     - `Semaine_1/`
     - `Semaine_2/`
     - ... `Semaine_7/`
   - `Periode_2/`
   - `Banque_Ressources/`

3. Noter l'ID du dossier racine

---

## Étape 3 : Configurer Make.com (10 min)

### 3.1 Créer le compte

1. https://make.com/register
2. Confirmer l'email

### 3.2 Créer le scénario minimal (version simplifiée)

**Modules à ajouter** :

```
1. Scheduler → Jeudi 18h00
2. Google Sheets (Search Rows) → Lire "Semaines"
3. OpenAI (GPT-4) → Générer cahier journal
4. Google Docs → Créer document
5. WhatsApp (optionnel) → Envoyer message
```

**Configuration rapide** :

**Module 2 - Google Sheets** :
- Spreadsheet : Choisir votre fichier
- Sheet : "Semaines"
- Filter : `Statut = À préparer`

**Module 3 - OpenAI** :
- API Key : Votre clé (commençant par `sk-`)
- Model : `gpt-4`
- System message : Copier depuis [`prompts/01-cahier-journal-prompt.md`](prompts/01-cahier-journal-prompt.md)
- User message :
  ```
  Période : {{2.periode}}
  Semaine : {{2.semaine}}
  Domaine : {{2.domaine}}
  Thème : {{2.theme}}
  Durée : {{2.duree}} minutes

  Génère un cahier journal complet pour cette séance.
  ```

**Module 4 - Google Docs** :
- Document name : `Cahier_{{2.periode}}_{{2.semaine}}`
- Content : `{{3.text}}`

**Module 5 - WhatsApp** (optionnel) :
- Message : `Cahier journal P{{2.periode}}S{{2.semaine}} prêt !`

---

## Étape 4 : Tester (5 min)

1. **Make.com** : Clic droit sur le scénario > "Run once"
2. **Vérifier** :
   - ✅ Document créé dans Drive ?
   - ✅ Message WhatsApp reçu ?
3. **Si ça marche** : Activer le scheduler (toggle ON)

---

## C'est tout ! 🎉

Votre système minimal est opérationnel.

**Prochaine étape** : Ajouter les fonctionnalités avancées
- 🎞️ Génération de slides
- 📄 Gestion des photocopies
- 🖼️ Images IA (DALL·E)

Voir le [guide complet d'installation](docs/guide-installation.md)

---

## Utilisation quotidienne

### Lundi/Mardi : Planifier la semaine

Ajouter une ligne dans "Semaines" :
```
P2S5 | P2 | 5 | 04/12/2024 | 07/12/2024 | Maths | La division | 50 | À préparer
```

### Jeudi 18h : Réception automatique

Vous recevez :
- 📘 Document Word (cahier journal)
- 💬 Message WhatsApp avec le lien

### Vendredi : Imprimer et enseigner

1. Ouvrir le document
2. Imprimer si besoin
3. Utiliser en classe !

---

## Support rapide

### Erreur "Permission denied"

➡️ Make.com > Connections > Google Sheets > Reauthorize

### Erreur "Invalid API key"

➡️ Vérifier que la clé OpenAI est correcte

### Le scénario ne se lance pas

➡️ Vérifier que le toggle est ON et que le scheduler est configuré

### Besoin d'aide ?

📖 [Guide complet](docs/guide-installation.md)
💬 [Forum de discussion](https://github.com/VOTRE_USERNAME/Moutouchi/discussions)

---

**Bon enseignement ! 🌿**
