# 📊 DASHBOARD METRICS EN TEMPS RÉEL - MOUTOUCHI

**Objectif** : Suivi automatique de TOUS les KPIs importants
**Temps setup** : 15 minutes
**Plateforme** : Google Sheets (gratuit)

---

## 🚀 SETUP RAPIDE (15 MIN)

### Étape 1 : Créer le Google Sheet (2 min)

1. Aller sur https://sheets.google.com
2. Créer nouveau fichier
3. Renommer : "MOUTOUCHI - Dashboard Metrics"
4. Créer 4 onglets :
   - `📊 Dashboard` (vue synthétique)
   - `📝 Données brutes` (entrées manuelles quotidiennes)
   - `📈 Graphiques` (visualisations)
   - `🎯 Objectifs` (cibles 30j/90j/1an)

---

## 📊 ONGLET 1 : DASHBOARD (vue principale)

### Layout

```
┌─────────────────────────────────────────────────────────┐
│  MOUTOUCHI - DASHBOARD TEMPS RÉEL                       │
│  Dernière màj : [AUTO]                                  │
├─────────────────────────────────────────────────────────┤
│  AUJOURD'HUI                                            │
│  ┌──────────┬──────────┬──────────┬──────────┐        │
│  │ Visiteurs│ Signups  │ MRR      │ Clients  │        │
│  │ 12       │ 3        │ 45€      │ 3        │        │
│  └──────────┴──────────┴──────────┴──────────┘        │
├─────────────────────────────────────────────────────────┤
│  CETTE SEMAINE                                          │
│  ┌──────────┬──────────┬──────────┬──────────┐        │
│  │ Visiteurs│ Signups  │ Conv%    │ Actifs   │        │
│  │ 87       │ 18       │ 20.7%    │ 12       │        │
│  └──────────┴──────────┴──────────┴──────────┘        │
├─────────────────────────────────────────────────────────┤
│  CE MOIS                                                │
│  ┌──────────┬──────────┬──────────┬──────────┐        │
│  │ Visiteurs│ Signups  │ MRR      │ Churn%   │        │
│  │ 342      │ 68       │ 75€      │ 2.1%     │        │
│  └──────────┴──────────┴──────────┴──────────┘        │
├─────────────────────────────────────────────────────────┤
│  OBJECTIFS 30J (Progress)                               │
│  Visiteurs : ████████░░░░ 68% (342/500)               │
│  Signups :   ████████████ 68% (68/100)                │
│  MRR :       ████████████████████ 100% (75€/75€) ✅   │
│  Actifs :    ████████░░░░ 60% (12/20)                 │
└─────────────────────────────────────────────────────────┘
```

### Formules

#### AUJOURD'HUI (cellule C3 = Visiteurs aujourd'hui)

```excel
=SUMIF('Données brutes'!A:A, TODAY(), 'Données brutes'!B:B)
```

**Explication** :
- `SUMIF` : Somme conditionnelle
- `'Données brutes'!A:A` : Colonne dates
- `TODAY()` : Date du jour
- `'Données brutes'!B:B` : Colonne visiteurs

#### CETTE SEMAINE (cellule C10 = Visiteurs cette semaine)

```excel
=SUMIFS('Données brutes'!B:B, 'Données brutes'!A:A, ">="&TODAY()-WEEKDAY(TODAY(),2), 'Données brutes'!A:A, "<="&TODAY())
```

**Explication** :
- `SUMIFS` : Somme avec plusieurs conditions
- `TODAY()-WEEKDAY(TODAY(),2)` : Lundi de cette semaine
- Entre lundi et aujourd'hui

#### TAUX DE CONVERSION % (cellule E10)

```excel
=IF(C10=0, 0, ROUND(D10/C10*100, 1))
```

**Explication** :
- Si visiteurs = 0 → 0% (évite division par 0)
- Sinon : (Signups / Visiteurs) × 100, arrondi à 1 décimale

#### PROGRESS BAR (cellule B23 = barre visiteurs)

```excel
=REPT("█", INT(C17/Objectifs!B2*20)) & REPT("░", 20-INT(C17/Objectifs!B2*20)) & " " & ROUND(C17/Objectifs!B2*100, 0) & "%"
```

**Explication** :
- `REPT("█", n)` : Répète █ n fois (partie remplie)
- `INT(C17/Objectifs!B2*20)` : Progression sur 20 caractères
- `REPT("░", ...)` : Partie vide
- Affiche % à la fin

#### MRR (Monthly Recurring Revenue) (cellule E17)

```excel
=SUMIF('Données brutes'!A:A, ">="&EOMONTH(TODAY(),-1)+1, 'Données brutes'!G:G)
```

**Explication** :
- `EOMONTH(TODAY(),-1)+1` : Premier jour du mois en cours
- Somme revenus depuis début du mois

#### CHURN % (cellule F17)

```excel
=IF(G16=0, 0, ROUND((G16-G17)/G16*100, 1))
```

**Explication** :
- (Clients mois dernier - Clients mois actuel) / Clients mois dernier × 100
- Si mois dernier = 0 → 0%

---

## 📝 ONGLET 2 : DONNÉES BRUTES

### Structure (colonnes A-M)

```
| A | B | C | D | E | F | G | H | I | J | K | L | M |
|Date|Visiteurs|Signups|Conv%|Actifs|Activ%|Clients|MRR|Churn%|NPS|CAC|Dépenses|Notes|
```

### Exemple de ligne (Jour 1)

```
| 2024-11-09 | 25 | 5 | 20% | 0 | 0% | 0 | 0€ | 0% | - | 0€ | 50€ | Lancement questionnaire |
```

### Formules auto-calculées

#### Taux de conversion % (colonne D, ligne 2)

```excel
=IF(B2=0, 0, ROUND(C2/B2*100, 1))
```

#### Taux d'activation % (colonne F, ligne 2)

```excel
=IF(C2=0, 0, ROUND(E2/C2*100, 1))
```

#### Churn % (colonne I, ligne 2)

```excel
=IF(G1=0, 0, ROUND((G1-G2)/G1*100, 1))
```

**Formule à copier jusqu'en bas** (sélectionner D2:D100, Ctrl+D)

---

### Données à saisir MANUELLEMENT chaque jour (10 min)

**Colonne A : Date**
```
=TODAY()
```
(puis figer la valeur : copier > coller valeurs)

**Colonne B : Visiteurs landing page**
Source : Google Analytics
→ Aller sur analytics.google.com
→ Rapports > Engagement > Pages
→ Noter visiteurs sur `/`

**Colonne C : Signups bêta**
Source : Google Forms réponses
→ Compter nouvelles lignes du jour

**Colonne E : Bêta actifs**
Source : Google Sheets "Semaines" (table générée)
→ Compter combien ont généré ≥1 semaine

**Colonne G : Clients payants**
Source : Stripe dashboard
→ Abonnements actifs

**Colonne H : MRR**
Formule auto :
```excel
=G2*15
```
(si tous Essentiel 15€) OU manuellement si mix Essentiel/Pro

**Colonne J : NPS (Net Promoter Score)**
Source : Questionnaire satisfaction (Q : "Note 0-10")
→ Moyenne du jour

**Colonne K : CAC (Customer Acquisition Cost)**
Formule auto :
```excel
=IF(G2-G1=0, 0, L2/(G2-G1))
```
**Explication** :
- Dépenses marketing jour / Nouveaux clients jour
- Si 0 nouveau client → CAC = 0

**Colonne L : Dépenses marketing**
Source : Factures
→ Facebook Ads + Google Ads du jour

**Colonne M : Notes**
Événements importants :
- "Lancement questionnaire"
- "Bug Make.com corrigé"
- "Partenariat école XYZ"
- "Post viral (50 partages)"

---

## 📈 ONGLET 3 : GRAPHIQUES

### Graphique 1 : Évolution visiteurs + signups (ligne)

**Données** :
- Axe X : `Données brutes!A:A` (dates)
- Série 1 : `Données brutes!B:B` (visiteurs, bleu)
- Série 2 : `Données brutes!C:C` (signups, vert)

**Type** : Courbe lissée (Smooth line chart)

**Config** :
- Titre : "Trafic et conversions (30 jours)"
- Axe Y gauche : Visiteurs
- Axe Y droit : Signups
- Légende : En haut

---

### Graphique 2 : Funnel de conversion (entonnoir)

**Données** :
```
Étape            | Valeur | % du précédent
─────────────────────────────────────────
Visiteurs        | 500    | 100%
Signups          | 100    | 20%
Actifs (ont testé)| 60    | 60%
Clients payants  | 5      | 8.3%
```

**Formules** :

Cellule C2 (% Signups) :
```excel
=ROUND(B2/B1*100, 1)
```

Cellule C3 (% Actifs) :
```excel
=ROUND(B3/B2*100, 1)
```

**Type** : Graphique en entonnoir (Funnel chart)
OU colonne empilée si pas dispo

---

### Graphique 3 : MRR progression (colonne)

**Données** :
- Axe X : Mois (Nov 2024, Déc 2024, Jan 2025...)
- Axe Y : MRR cumulé (0€, 75€, 300€, 750€...)

**Type** : Histogramme (Column chart)

**Objectif superposé** :
- Ligne horizontale à 3000€ (objectif An 1)
- Couleur rouge pointillée

---

### Graphique 4 : Répartition clients (camembert)

**Données** :
```
Offre       | Clients | %
──────────────────────────
Gratuit     | 80      | 80%
Essentiel   | 15      | 15%
Pro         | 5       | 5%
```

**Type** : Pie chart (camembert)

**Couleurs** :
- Gratuit : Gris (#95A5A6)
- Essentiel : Vert (#16A085)
- Pro : Orange (#E67E22)

---

### Graphique 5 : NPS évolution (jauge)

**Données** :
- NPS moyen des 7 derniers jours

**Formule** :
```excel
=AVERAGE(FILTER('Données brutes'!J:J, 'Données brutes'!A:A >= TODAY()-7))
```

**Type** : Gauge chart (jauge) OU colonne simple

**Zones** :
- 0-6 : Rouge (détracteurs)
- 7-8 : Orange (passifs)
- 9-10 : Vert (promoteurs)

---

## 🎯 ONGLET 4 : OBJECTIFS

### Structure

```
| Métrique | Objectif 30j | Objectif 90j | Objectif An 1 |
|----------|-------------|--------------|---------------|
| Visiteurs landing | 500 | 2000 | 10000 |
| Signups bêta | 100 | - | - |
| Taux conversion | 20% | 25% | 30% |
| Bêta actifs | 20 | - | - |
| Taux activation | 60% | 70% | 80% |
| Clients payants | 5 | 50 | 200 |
| MRR | 75€ | 750€ | 3000€ |
| Churn % | <5% | <3% | <2% |
| NPS | 8/10 | 8.5/10 | 9/10 |
| CAC | <30€ | <20€ | <15€ |
```

### Formules de comparaison (colonne E = "Statut")

```excel
=IF(Dashboard!C17 >= B2, "✅ Atteint", IF(Dashboard!C17 >= B2*0.8, "⚠️ Proche", "❌ Loin"))
```

**Explication** :
- Si réalisé ≥ objectif → ✅
- Si réalisé ≥ 80% objectif → ⚠️
- Sinon → ❌

---

## 🤖 AUTOMATISATIONS (niveau avancé)

### Auto-fetch Google Analytics (avec Apps Script)

**Code Google Apps Script** (Outils > Éditeur de script)

```javascript
function fetchGoogleAnalytics() {
  // Remplacer par ton ID Google Analytics
  var viewId = 'ga:XXXXXXXXX';

  var startDate = Utilities.formatDate(new Date(), 'GMT', 'yyyy-MM-dd');
  var endDate = startDate;

  var metrics = 'ga:users';
  var dimensions = 'ga:date';

  var results = Analytics.Data.Ga.get(
    viewId,
    startDate,
    endDate,
    metrics,
    {dimensions: dimensions}
  );

  if (results.rows && results.rows.length > 0) {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Données brutes');
    var lastRow = sheet.getLastRow() + 1;

    // Écrire visiteurs dans colonne B
    sheet.getRange(lastRow, 2).setValue(results.rows[0][1]);
  }
}
```

**Setup** :
1. Outils > Éditeur de script
2. Copier code ci-dessus
3. Remplacer `ga:XXXXXXXXX` par ton ID Analytics
4. Enregistrer
5. Déclencheurs > Ajouter déclencheur > fetchGoogleAnalytics > Quotidien (9h-10h)

---

### Auto-fetch Stripe MRR (avec Zapier gratuit)

**Flow** :
1. Trigger : Zapier Schedule (tous les jours 10h)
2. Action : Stripe "Get All Subscriptions"
3. Action : Google Sheets "Update Cell" (colonne H, ligne du jour)

**Config** :
- Zapier gratuit : 100 tâches/mois (suffisant)
- Stripe API key : Obtenir dans Dashboard > Developers > API keys

---

### Alertes automatiques (via formules)

**Cellule alerte Dashboard** (A1) :

```excel
=IF(Dashboard!C17 < Objectifs!B2*0.5, "🚨 ALERTE : Objectif MRR très loin (< 50%)",
   IF(Dashboard!I17 > 5, "⚠️ ATTENTION : Churn élevé (>5%)",
   "✅ Tout va bien"))
```

**Formule email notification** (avec Apps Script) :

```javascript
function checkAlertsAndEmail() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Dashboard');
  var alert = sheet.getRange('A1').getValue();

  if (alert.includes('ALERTE') || alert.includes('ATTENTION')) {
    MailApp.sendEmail({
      to: 'ton-email@example.com',
      subject: '🚨 MOUTOUCHI Alert',
      body: alert
    });
  }
}
```

**Setup déclencheur** : Quotidien à 18h

---

## 📊 MÉTRIQUES AVANCÉES (calculs)

### LTV (Lifetime Value)

**Formule** :
```excel
=AVERAGE('Données brutes'!H:H) / (AVERAGE('Données brutes'!I:I)/100)
```

**Explication** :
- LTV = MRR moyen / Churn % moyen
- Exemple : 15€ / 0.03 = 500€ (un client rapporte 500€ en moyenne sur sa durée de vie)

### Ratio LTV/CAC

**Formule** :
```excel
=LTV / AVERAGE('Données brutes'!K:K)
```

**Objectif** : ≥ 3 (idéalement ≥ 5)
- Si < 3 → Business pas rentable (coûte trop cher d'acquérir clients)
- Si ≥ 5 → Très sain

### Payback period (mois pour récupérer CAC)

**Formule** :
```excel
=AVERAGE('Données brutes'!K:K) / AVERAGE('Données brutes'!H:H)
```

**Explication** :
- CAC moyen / MRR par client
- Exemple : 30€ / 15€ = 2 mois
- Objectif : ≤ 6 mois

### Runway (combien de mois avant d'être à court d'argent)

**Formule** (si capital de départ = 5000€) :

```excel
=(5000 - SUM('Données brutes'!L:L)) / AVERAGE(FILTER('Données brutes'!L:L, 'Données brutes'!A:A >= TODAY()-30))
```

**Explication** :
- (Capital restant) / (Dépenses mensuelles moyennes)
- Exemple : 4200€ / 400€ = 10.5 mois de runway

---

## 🎨 FORMATAGE CONDITIONNEL

### Colonne MRR (vert si >objectif, rouge si <50%)

**Règle 1 (vert)** :
- Plage : `H2:H100`
- Condition : `>= Objectifs!$B$7`
- Format : Fond vert clair (#D5F4E6), texte vert foncé (#16A085)

**Règle 2 (rouge)** :
- Plage : `H2:H100`
- Condition : `< Objectifs!$B$7 * 0.5`
- Format : Fond rouge clair (#F9EBEA), texte rouge (#E74C3C)

### Colonne Churn % (rouge si >5%)

**Règle** :
- Plage : `I2:I100`
- Condition : `> 5`
- Format : Fond rouge, texte blanc, gras

### Colonne NPS (échelle couleur 0-10)

**Règle échelle de couleurs** :
- Plage : `J2:J100`
- Échelle : Rouge (0) → Jaune (5) → Vert (10)

---

## ✅ CHECKLIST SETUP DASHBOARD

**Étape 1 : Structure (5 min)**
- [ ] Créer Google Sheet "MOUTOUCHI - Dashboard"
- [ ] Créer 4 onglets (Dashboard, Données brutes, Graphiques, Objectifs)

**Étape 2 : Formules (5 min)**
- [ ] Copier formules Dashboard (cellules C3, C10, E10, B23, E17, F17)
- [ ] Copier formules Données brutes (colonnes D, F, I)
- [ ] Vérifier qu'aucune erreur #REF!

**Étape 3 : Graphiques (3 min)**
- [ ] Créer graphique 1 (Visiteurs + Signups)
- [ ] Créer graphique 2 (Funnel)
- [ ] Créer graphique 3 (MRR progression)

**Étape 4 : Objectifs (1 min)**
- [ ] Copier tableau objectifs (30j, 90j, An 1)

**Étape 5 : Première saisie (1 min)**
- [ ] Remplir ligne Jour 1 (Données brutes)
- [ ] Vérifier Dashboard affiche correctement

---

## 🔥 UTILISATION QUOTIDIENNE (10 MIN/JOUR)

### Routine matinale (9h00)

1. **Ouvrir Dashboard Google Sheets**
2. **Aller sur onglet "Données brutes"**
3. **Créer nouvelle ligne (date du jour)**
4. **Saisir metrics** :
   - Visiteurs (Google Analytics)
   - Signups (Google Forms)
   - Bêta actifs (Google Sheets "Semaines")
   - Clients payants (Stripe)
   - MRR (auto-calculé)
   - Dépenses (factures Facebook Ads)
   - Notes (événements marquants)
5. **Vérifier onglet "Dashboard"**
   - Alertes en rouge ?
   - Objectifs atteints ?
   - Tendances à la hausse/baisse ?
6. **Screenshot dashboard** (pour archives)
7. **Ajuster actions du jour** (si metrics mauvais)

### Analyse hebdomadaire (dimanche 18h, 30 min)

1. **Comparer semaine vs semaine précédente**
   - Visiteurs : +X% ?
   - Conversion : +X% ?
   - MRR : +X€ ?

2. **Identifier top 3 insights** :
   - Exemple : "Post Facebook généré 50% du trafic"
   - Exemple : "Taux activation baisse (60% → 45%)"
   - Exemple : "CAC augmente (20€ → 35€)"

3. **Décider 3 actions semaine suivante** :
   - Exemple : "Poster 2× plus sur Facebook"
   - Exemple : "Améliorer onboarding bêta (vidéo tuto)"
   - Exemple : "Réduire dépenses Google Ads (pas rentable)"

4. **Noter dans colonne M (Notes)** :
   - "Semaine 2 : Focus Facebook, réduction Google Ads"

---

## 📱 VERSION MOBILE (Google Sheets app)

**Dashboard simplifié mobile** (vue onglet séparé "📱 Mobile")

```
AUJOURD'HUI
──────────────
Visiteurs : 12
Signups : 3
MRR : 45€

SEMAINE
──────────────
Visiteurs : 87
Conv% : 20.7%
MRR : 45€

ALERTE
──────────────
✅ Tout va bien
```

**Formules identiques**, juste layout vertical pour mobile

---

## 🎁 TEMPLATES GOOGLE SHEETS

### Template 1 : Dashboard minimaliste (10 metrics)

**Colonnes** : Date, Visiteurs, Signups, Conv%, MRR, Clients, Churn%, Notes

**Graphiques** : 2 (Visiteurs+Signups, MRR progression)

**Temps** : 10 min setup

---

### Template 2 : Dashboard complet (20 metrics)

**Colonnes** : Date, Visiteurs, Signups, Conv%, Actifs, Activ%, Clients, MRR, Churn%, NPS, CAC, LTV, Ratio LTV/CAC, Dépenses, Runway, Notes

**Graphiques** : 5 (trafic, funnel, MRR, NPS, CAC)

**Temps** : 30 min setup

---

## 🚀 PRÊT !

Tu as maintenant :
- ✅ Dashboard Google Sheets complet
- ✅ Formules auto-calculées (conv%, churn%, CAC...)
- ✅ 5 graphiques de visualisation
- ✅ Alertes conditionnelles
- ✅ Routine quotidienne 10 min
- ✅ Objectifs 30j/90j/An1

**Prochaine étape** :
1. Créer Google Sheet (5 min)
2. Copier formules (5 min)
3. Remplir Jour 1 (2 min)
4. Observer évolution quotidienne ! 📈

---

**Impact** : Décisions data-driven > Intuitions

**LET'S TRACK ! 📊**
