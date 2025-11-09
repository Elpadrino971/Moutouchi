# Guide d'installation complet - CM1 MOUTOUCHI

Ce guide vous accompagne pas à pas dans l'installation complète du système CM1 MOUTOUCHI.

**Durée estimée** : 1h - 1h30

---

## Étape 1 : Créer les comptes nécessaires (15 min)

### 1.1 Google Workspace

**Si vous avez déjà un compte Google** : Passez à l'étape suivante

**Sinon** :
1. Créer un compte Google : https://accounts.google.com/signup
2. Pour enseignants : demander un compte Google Workspace Education (gratuit)
   - https://edu.google.com/workspace-for-education/

### 1.2 Make.com

1. Aller sur https://make.com/register
2. Créer un compte gratuit (email + mot de passe)
3. Confirmer l'email
4. **Plan gratuit** : 1 000 opérations/mois (suffisant pour 4-5 semaines)

### 1.3 OpenAI

1. Aller sur https://platform.openai.com/signup
2. Créer un compte
3. Ajouter une méthode de paiement (carte bancaire)
4. Créer une clé API :
   - https://platform.openai.com/api-keys
   - Cliquer "Create new secret key"
   - **IMPORTANT** : Copier la clé et la sauvegarder (vous ne la reverrez plus)
   - Format : `sk-proj-...`

**Budget recommandé** :
- Définir une limite à 20€/mois (Settings > Billing > Usage limits)

### 1.4 Twilio (optionnel - pour WhatsApp)

1. Aller sur https://twilio.com/try-twilio
2. Créer un compte gratuit
3. Vérifier votre numéro de téléphone
4. Activer WhatsApp Sandbox :
   - Console > Messaging > Try it out > Send a WhatsApp message
   - Envoyer le code d'activation depuis votre WhatsApp
5. Noter :
   - Account SID
   - Auth Token
   - Numéro WhatsApp Twilio : `whatsapp:+14155238886`

**Alternative gratuite** : Utiliser Email au lieu de WhatsApp

---

## Étape 2 : Créer la base de données Google Sheets (20 min)

### 2.1 Créer le fichier principal

1. Aller sur https://sheets.google.com
2. Créer un nouveau fichier : "CM1_MOUTOUCHI_Database"
3. **Important** : Noter l'ID du fichier
   - URL : `https://docs.google.com/spreadsheets/d/{ID}/edit`
   - Copier `{ID}` et le sauvegarder

### 2.2 Créer l'onglet "Semaines"

1. Renommer "Sheet1" en "Semaines"
2. Créer les colonnes suivantes (ligne 1) :

```
A: ID
B: Période
C: Semaine
D: Date_Debut
E: Date_Fin
F: Domaine_Principal
G: Theme
H: Duree
I: Statut
J: Generee_Le
K: Lien_Cahier_Journal
L: Lien_PowerPoint
M: Lien_Photocopies
N: WhatsApp_Envoye
O: Remarques
```

3. **Validation des données** :

**Colonne F (Domaine_Principal)** :
- Sélectionner colonne F (de F2 à F100)
- Données > Validation de données
- Critères : Liste d'éléments
- Valeurs : `Français,Maths,Sciences,EMC,Anglais`

**Colonne I (Statut)** :
- Sélectionner colonne I
- Validation de données > Liste
- Valeurs : `À préparer,En cours,Générée,Terminée`

4. **Ajouter une ligne de test** :

```
P2S4 | P2 | 4 | 27/11/2024 | 30/11/2024 | Français | Identifier le groupe sujet | 45 | À préparer | | | | | | Contexte: marché
```

### 2.3 Créer l'onglet "Groupes"

1. Créer un nouvel onglet : "Groupes"
2. Colonnes :

```
A: Domaine
B: Nom_Groupe
C: Niveau
D: Effectif
E: Couleur
F: Icone
G: Description
H: Actif
```

3. **Ajouter les groupes** (exemple Français) :

```csv
Français,Aïmara,Débutant,7,#E74C3C,🌺,Besoin de reformulation,TRUE
Français,Angélique,Intermédiaire,10,#F39C12,🌻,Autonomie croissante,TRUE
Français,Sablier,Avancé,8,#27AE60,🌿,Très à l'aise,TRUE
```

4. **Répéter pour** Maths, Sciences, Anglais (voir `database-schemas/02-table-groupes.md`)

### 2.4 Créer l'onglet "Ressources"

1. Créer un nouvel onglet : "Ressources"
2. Colonnes :

```
A: ID_Ressource
B: Domaine
C: Type
D: Titre
E: Description
F: Lien_Drive
G: Niveau
H: Groupe_Cible
I: Periode
J: Semaine
K: Contexte_Guyane
L: Date_Ajout
M: Auteur
N: Tags
O: Actif
```

3. **Ajouter quelques ressources de test** (voir `database-schemas/03-table-ressources.md`)

### 2.5 Créer l'onglet "Photocopies"

1. Créer un nouvel onglet : "Photocopies"
2. Colonnes :

```
A: Semaine_ID
B: Domaine
C: Titre_Fiche
D: Lien_Drive
E: Groupe_Concerne
F: Quantite
G: Type_Document
H: Priorite
I: Imprime
J: Date_Impression
K: Remarques
```

3. **Laisser vide** (sera rempli automatiquement par Make)

### 2.6 Créer l'onglet "Logs" (optionnel mais recommandé)

1. Créer un nouvel onglet : "Logs"
2. Colonnes :

```
A: Date
B: Scenario
C: Statut
D: Message
E: Erreur
```

---

## Étape 3 : Créer la structure Google Drive (10 min)

### 3.1 Créer le dossier racine

1. Aller sur https://drive.google.com
2. Créer un dossier : "CM1_MOUTOUCHI"
3. **Noter l'ID** :
   - Ouvrir le dossier
   - URL : `https://drive.google.com/drive/folders/{ID}`
   - Copier `{ID}`

### 3.2 Créer les sous-dossiers

**Structure recommandée** :

```
CM1_MOUTOUCHI/
├── Periode_1/
│   ├── Semaine_1/
│   ├── Semaine_2/
│   ├── Semaine_3/
│   ├── Semaine_4/
│   ├── Semaine_5/
│   ├── Semaine_6/
│   └── Semaine_7/
├── Periode_2/
│   └── (même structure)
├── Periode_3/
│   └── (même structure)
├── Periode_4/
│   └── (même structure)
├── Periode_5/
│   └── (même structure)
└── Banque_Ressources/
    ├── Dictees/
    ├── Calcul_Mental/
    ├── Problemes/
    ├── Fiches_Manipulation/
    └── Images_Guyane/
```

**Pour créer rapidement** :

1. Créer `Periode_1` avec toutes les semaines (1-7)
2. Dupliquer `Periode_1` et renommer en `Periode_2`, `Periode_3`, etc.
3. Créer `Banque_Ressources` avec sous-dossiers

### 3.3 Noter les IDs importants

**Créer un document texte** "IDs_Drive.txt" avec :

```
SPREADSHEET_ID: [ID de votre Google Sheets]
DRIVE_FOLDER_ROOT: [ID du dossier CM1_MOUTOUCHI]
PERIODE_1_FOLDER: [ID du dossier Periode_1]
PERIODE_2_FOLDER: [ID du dossier Periode_2]
...
```

---

## Étape 4 : Configurer Make.com (30 min)

### 4.1 Créer le premier scénario

1. Se connecter à https://make.com
2. Cliquer "Create a new scenario"
3. Nom : `CM1_MOUTOUCHI_Generation_Hebdo`

### 4.2 Ajouter les modules (suivre `make-scenarios/scenario-1-generation-hebdomadaire.md`)

**Modules à ajouter dans l'ordre** :

1. **Scheduler** (déclencheur)
   - Rechercher "Schedule"
   - Configurer : Jeudi 18h00

2. **Google Sheets - Search Rows**
   - Connexion : Se connecter à Google (autoriser)
   - Spreadsheet : Choisir "CM1_MOUTOUCHI_Database"
   - Sheet : "Semaines"
   - Filter : `Statut = À préparer`

3. **Router** (condition)
   - Ajouter 2 routes :
     - Route 1 : `{{2.id}} is not empty`
     - Route 2 : `{{2.id}} is empty` → Stop

4. **Google Sheets - Search Rows** (Groupes)
   - Sheet : "Groupes"
   - Filter : `Domaine = {{2.domaine}}` AND `Actif = true`

5. **Google Sheets - Search Rows** (Ressources)
   - Sheet : "Ressources"
   - Filter : `Periode = {{2.periode}}` AND `Semaine = {{2.semaine}}` AND `Actif = true`

6. **Tools - Create JSON** (Groupes)
   - Voir détails dans le scénario

7. **Tools - Create JSON** (Ressources)
   - Voir détails dans le scénario

8. **OpenAI - Create a Completion** (Cahier Journal)
   - Connexion : Ajouter votre clé API OpenAI
   - Model : `gpt-4`
   - System message : Copier depuis `prompts/01-cahier-journal-prompt.md`
   - User message : Utiliser les variables `{{2.periode}}`, `{{2.semaine}}`, etc.

9. **Google Docs - Create Document from Text**
   - Nom : `Cahier_Journal_{{2.periode}}_{{2.semaine}}_{{2.domaine}}`
   - Content : `{{8.text}}`

10. **OpenAI - Create a Completion** (Slides)
    - System message : Copier depuis `prompts/02-slides-prompt.md`
    - Response format : JSON

11. **OpenAI - Create Image** (DALL·E) — OPTIONNEL
    - Model : `dall-e-3`
    - Prompt : `{{10.slide1.bg_prompt}}`
    - Répéter 8 fois (ou utiliser Iterator)

12. **Google Slides - Create Presentation**
    - À faire via API (voir documentation)

13. **Google Sheets - Add Rows** (Photocopies)
    - Iterator sur les ressources
    - Ajouter ligne par ligne

14. **Google Drive - Move File** (x2)
    - Déplacer Docs et Slides vers le bon dossier

15. **Google Sheets - Update Row** (Semaines)
    - Mettre à jour avec les liens + statut "Générée"

16. **Twilio - Send WhatsApp Message** (optionnel)
    - From : `whatsapp:+14155238886`
    - To : `whatsapp:+594XXXXXXXXX`
    - Body : Message récapitulatif

### 4.3 Tester le scénario

1. **Avant de lancer** : Vérifier que la ligne de test existe dans "Semaines"
2. Clic droit sur le scénario > "Run once"
3. Observer l'exécution (chaque module doit être vert)
4. **Si erreur** :
   - Cliquer sur le module en erreur
   - Lire le message
   - Corriger
   - Relancer

5. **Vérifier les sorties** :
   - Document Word créé dans Drive ?
   - PowerPoint créé ?
   - Photocopies remplies ?
   - WhatsApp reçu ?

### 4.4 Activer le scheduler

Une fois que tout fonctionne :
1. Toggle "ON" en bas du scénario
2. Le scénario s'exécutera automatiquement chaque jeudi à 18h

---

## Étape 5 : Créer le second scénario (Rappel photocopies) (10 min)

1. Créer un nouveau scénario : `CM1_MOUTOUCHI_Rappel_Photocopies`
2. Suivre `make-scenarios/scenario-2-rappel-photocopies.md`
3. Beaucoup plus simple (6 modules seulement)
4. Tester
5. Activer

---

## Étape 6 : Vérification finale (5 min)

### Checklist complète

- ✅ Google Sheets créé avec 4 onglets (Semaines, Groupes, Ressources, Photocopies)
- ✅ Données de test ajoutées
- ✅ Structure Drive créée (Periode_1, Periode_2, etc.)
- ✅ Scénario 1 créé et testé
- ✅ Scénario 2 créé et testé
- ✅ Connexions configurées (Google, OpenAI, Twilio)
- ✅ Schedulers activés
- ✅ Message WhatsApp de test reçu

---

## Dépannage

### Problème : "Permission denied" (Google Sheets)

**Solution** :
- Make.com > Connections > Google Sheets
- Cliquer "Reauthorize"
- Accepter toutes les permissions

### Problème : "Invalid API key" (OpenAI)

**Solution** :
- Vérifier que la clé commence par `sk-`
- Vérifier qu'elle n'a pas expiré
- Régénérer une nouvelle clé si besoin

### Problème : "Quota exceeded" (OpenAI)

**Solution** :
- Vérifier votre solde sur https://platform.openai.com/usage
- Ajouter des crédits si nécessaire
- Ou attendre le reset mensuel

### Problème : "File not found" (Drive)

**Solution** :
- Vérifier que les IDs de dossiers sont corrects
- Vérifier que Make a accès au Drive (permissions)

---

## Aller plus loin

### Optimisations

1. **Réduire les coûts OpenAI** :
   - Utiliser GPT-3.5-turbo pour les brouillons
   - Utiliser Unsplash au lieu de DALL·E pour les images

2. **Améliorer les prompts** :
   - Ajouter des exemples spécifiques à votre classe
   - Adapter le vocabulaire
   - Affiner la différenciation

3. **Ajouter des fonctionnalités** :
   - Génération de feedback élèves
   - Rapport de période
   - Export PDF automatique

### Support

Si vous êtes bloqué :
- 📖 Consulter la [FAQ](faq.md)
- 💬 Poster sur les [Discussions GitHub](https://github.com/VOTRE_USERNAME/Moutouchi/discussions)
- 📧 Envoyer un email : votre.email@exemple.com

---

**Félicitations ! Votre système CM1 MOUTOUCHI est opérationnel 🎉**
