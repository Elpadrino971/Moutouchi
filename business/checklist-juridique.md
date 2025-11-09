# Checklist juridique - MOUTOUCHI

**Objectif** : Assurer la conformité légale minimale avant de lancer

---

## ⚠️ DISCLAIMER IMPORTANT

> Je ne suis pas avocat. Cette checklist est indicative.
> Consultez un professionnel du droit si nécessaire.

**Pour un MVP** : Les points 1-5 suffisent.
**Pour un lancement commercial** : Tous les points sont recommandés.

---

## 🟢 PRIORITÉ 1 : ESSENTIEL (avant de collecter des emails)

### 1. Mentions légales (obligatoire)

**Où** : Footer de votre landing page

**Contenu minimum** :

```
MENTIONS LÉGALES

Éditeur :
[Votre prénom] [Votre nom]
[Votre adresse]
Email : contact@moutouchi.com
Téléphone : +594 XXX XXX XXX

Hébergement :
Carrd.co (ou Google Sites, etc.)
[Adresse hébergeur]

Directeur de publication :
[Votre nom]

---

© 2024 MOUTOUCHI - Tous droits réservés
```

**Statut légal** :
- En bêta : Pas besoin de créer une société
- Vous opérez en **nom propre** (auto-entrepreneur ou particulier)

---

### 2. Politique de confidentialité (RGPD)

**Où** : Page dédiée sur votre site

**Template simplifié** :

```
POLITIQUE DE CONFIDENTIALITÉ

Dernière mise à jour : [Date]

1. DONNÉES COLLECTÉES

Nous collectons :
- Prénom, email (via formulaire d'inscription)
- Données d'utilisation (via Google Analytics)

Nous NE collectons PAS :
- Données nominatives d'élèves
- Informations bancaires (gérées par Stripe)

2. UTILISATION DES DONNÉES

Vos données servent à :
- Vous envoyer les accès au produit
- Améliorer le service
- Vous envoyer des emails (avec consentement)

3. VOS DROITS (RGPD)

Vous pouvez à tout moment :
- Accéder à vos données (contact@moutouchi.com)
- Modifier vos données
- Supprimer vos données
- Vous désabonner des emails (lien en bas de chaque email)

4. STOCKAGE

Vos données sont stockées :
- Sur Google Sheets (données UE)
- Sur Stripe (paiements, données UE)
- Sur Make.com (automatisation, données UE)

Durée de conservation : 3 ans après dernier contact

5. COOKIES

Nous utilisons Google Analytics (cookies de mesure d'audience).
Vous pouvez les refuser via votre navigateur.

6. CONTACT

Pour toute question : contact@moutouchi.com
```

**Outils gratuits pour générer** :
- https://www.cnil.fr/fr/generer-une-politique-de-confidentialite
- https://www.gdprprivacypolicy.net (EN)

---

### 3. Consentement RGPD

**Dans le formulaire d'inscription** :

Ajouter une case à cocher (obligatoire) :

```
☐ J'accepte de recevoir des emails de MOUTOUCHI concernant le produit et les nouveautés.
☐ J'ai lu et j'accepte la Politique de confidentialité [lien]
```

**Important** : La case doit être **décochée par défaut** (opt-in actif).

---

### 4. CGV (Conditions Générales de Vente)

**Quand** : Avant de facturer (pas nécessaire en bêta gratuite)

**Template simplifié** :

```
CONDITIONS GÉNÉRALES DE VENTE

1. OBJET

MOUTOUCHI propose un service d'automatisation de préparations pédagogiques par abonnement.

2. TARIFS

- Gratuit : 2 générations/mois
- Essentiel : 15€/mois TTC
- Pro : 30€/mois TTC

Les prix peuvent être modifiés avec un préavis de 30 jours.

3. PAIEMENT

Paiements sécurisés via Stripe.
Prélèvement automatique mensuel.

4. DURÉE ET RÉSILIATION

Abonnement sans engagement.
Résiliation possible à tout moment (effet immédiat).
Aucun remboursement au prorata.

5. GARANTIE

Nous garantissons un taux de disponibilité de 95%.
En cas de bug, nous nous engageons à corriger sous 7 jours.

6. RESPONSABILITÉ

MOUTOUCHI est un outil d'aide à la préparation.
L'enseignant reste responsable du contenu pédagogique utilisé en classe.

7. PROPRIÉTÉ INTELLECTUELLE

Les documents générés vous appartiennent.
Vous pouvez les utiliser librement en classe.

8. DONNÉES PERSONNELLES

Voir Politique de confidentialité.

9. LITIGE

Loi française applicable.
Tribunal compétent : Cayenne (Guyane).

10. CONTACT

Email : contact@moutouchi.com
```

**Outils gratuits pour générer** :
- https://www.assistant-juridique.fr/cgv.jsp
- https://www.legalplace.fr/contrats/cgv-saas/

---

### 5. CGU (Conditions Générales d'Utilisation)

**Quand** : Dès que le service est accessible

**Template simplifié** :

```
CONDITIONS GÉNÉRALES D'UTILISATION

1. ACCEPTATION

En utilisant MOUTOUCHI, vous acceptez ces CGU.

2. DESCRIPTION DU SERVICE

MOUTOUCHI génère automatiquement des documents pédagogiques via IA.
Nous ne garantissons pas une exactitude à 100%.

3. UTILISATION ACCEPTABLE

Vous vous engagez à :
- Utiliser le service de bonne foi
- Ne pas tenter de pirater le système
- Ne pas revendre les documents générés
- Respecter le droit d'auteur

4. PROPRIÉTÉ INTELLECTUELLE

Le code et les prompts IA appartiennent à MOUTOUCHI.
Les documents générés vous appartiennent.

5. SUSPENSION / RÉSILIATION

Nous pouvons suspendre un compte en cas d'usage abusif (spam, piratage).

6. LIMITATION DE RESPONSABILITÉ

MOUTOUCHI est fourni "en l'état".
Nous ne sommes pas responsables des erreurs pédagogiques éventuelles.

7. MODIFICATIONS

Nous pouvons modifier ces CGU avec un préavis de 15 jours (email).

8. CONTACT

Email : contact@moutouchi.com
```

---

## 🟡 PRIORITÉ 2 : RECOMMANDÉ (avant le lancement commercial)

### 6. Créer une structure juridique

**Options** :

**Micro-entreprise (auto-entrepreneur)** :
- ✅ Simple et rapide (1h en ligne)
- ✅ Pas de capital requis
- ✅ Comptabilité simplifiée
- ❌ Plafond de CA : 77 700€/an (services)
- ❌ Pas d'associés possibles

**SASU (Société par Actions Simplifiée Unipersonnelle)** :
- ✅ Pas de plafond de CA
- ✅ Image plus professionnelle
- ✅ Possibilité de lever des fonds
- ❌ Plus cher (500€ création)
- ❌ Comptabilité complexe (expert-comptable)

**Conseil** :
- **An 1** : Micro-entreprise (ou rester particulier si < 5k€/an)
- **An 2+** : SASU si CA > 50k€

**Démarches micro-entreprise** :
1. Aller sur https://www.autoentrepreneur.urssaf.fr
2. Créer un compte
3. Remplir le formulaire (15 min)
4. Recevoir SIRET (sous 15 jours)

**Coût** : Gratuit

---

### 7. Assurance responsabilité professionnelle

**Pourquoi** :
En cas de problème (bug causant un préjudice à un enseignant), vous êtes couvert.

**Coût** : ~20-50€/mois

**Assureurs** :
- Hiscox : https://www.hiscox.fr
- AXA Pro : https://www.axa.fr/pro
- Macif Pro

**Obligatoire ?** Non, mais fortement recommandé.

---

### 8. Déclaration CNIL (données personnelles)

**Quand** : Si vous traitez des données sensibles (âge, origine, etc.)

**Pour MOUTOUCHI** :
- Pas de données sensibles d'élèves stockées
- Seulement emails enseignants + Google Analytics
- **Pas de déclaration CNIL nécessaire** (sous réserve)

**Mais** : Tenir un **registre des traitements** (RGPD)

**Template registre** :
```
REGISTRE DES TRAITEMENTS

Traitement 1 : Newsletter
- Finalité : Envoyer emails produit
- Données : Email, prénom
- Stockage : Mailchimp (UE)
- Durée : 3 ans
- Base légale : Consentement

Traitement 2 : Analytics
- Finalité : Mesurer audience
- Données : IP (anonymisée), pages vues
- Stockage : Google Analytics (UE)
- Durée : 26 mois
- Base légale : Intérêt légitime
```

**Outil gratuit** : https://www.cnil.fr/fr/RGDPF

---

### 9. Numéro de TVA intracommunautaire

**Quand** : Si vous vendez en B2B en Europe

**Pour MOUTOUCHI** :
- B2C (enseignants individuels) : Pas nécessaire si micro-entreprise
- B2B (écoles/rectorats) : Nécessaire si > 10k€/an

**Obtenir un numéro de TVA** :
1. Créer micro-entreprise (ou SASU)
2. Demander à l'URSSAF ou SIE
3. Délai : 15 jours

**Format** : `FR XX XXXXXXXXX`

---

### 10. Contrat de prestation (B2B)

**Quand** : Si vous vendez à une école ou un rectorat

**Contenu minimum** :
- Parties (vous + établissement)
- Objet (abonnement MOUTOUCHI)
- Durée (1 an renouvelable)
- Prix (100€/mois par exemple)
- Modalités de paiement (virement, mandat)
- Conditions de résiliation (préavis 3 mois)

**Template** : Voir un avocat ou utiliser LegalPlace

---

## 🔴 PRIORITÉ 3 : SI BESOIN (croissance avancée)

### 11. Dépôt de marque

**Quand** : Si vous voulez protéger le nom "MOUTOUCHI"

**Coût** : 190€ (INPI)

**Démarches** :
1. Vérifier disponibilité : https://bases-marques.inpi.fr
2. Déposer en ligne : https://www.inpi.fr

**Classes à déposer** :
- Classe 9 : Logiciels
- Classe 41 : Éducation, formation

**Conseil** : Attendre 50+ clients avant de déposer

---

### 12. Droit d'auteur (code source)

**Par défaut** :
Le code que vous écrivez vous appartient automatiquement (droit d'auteur).

**Licence open-source** (si vous voulez partager) :
- MIT License (très permissive)
- GPL (copyleft)

**Pour MOUTOUCHI** :
Si vous voulez garder propriétaire → Pas de licence open-source

---

### 13. Accord de confidentialité (NDA)

**Quand** : Si vous travaillez avec des développeurs ou partenaires

**Template** : LegalPlace, Rocket Lawyer

**Pour MOUTOUCHI** :
Pas nécessaire en solo. Si vous embauchez → NDA avant de partager le code.

---

## ✅ RÉCAPITULATIF : QUE FAIRE MAINTENANT ?

### En bêta gratuite (0€ de CA)

- [x] Mentions légales ✅
- [x] Politique de confidentialité ✅
- [x] Consentement RGPD (case à cocher) ✅
- [ ] CGU (optionnel mais recommandé)
- [ ] Créer micro-entreprise (optionnel)

**Total coût** : 0€
**Temps** : 2-3h

---

### En lancement commercial (<10k€ CA/an)

- [x] Tout ce qui précède
- [x] CGV (obligatoire) ✅
- [x] Créer micro-entreprise ✅
- [x] Assurance RC Pro (recommandé) ✅
- [ ] Déclaration CNIL (si besoin)

**Total coût** : ~300€/an (assurance)
**Temps** : 5-6h

---

### En croissance (>10k€ CA/an)

- [x] Tout ce qui précède
- [x] SASU (au lieu de micro) ✅
- [x] Expert-comptable ✅
- [x] Dépôt de marque ✅
- [x] Contrats B2B formalisés ✅

**Total coût** : ~2 000€/an (comptable + marque)

---

## 🛡️ PROTECTION DES DONNÉES (RGPD)

### Principes clés

1. **Minimisation** : Ne collectez que ce dont vous avez besoin
2. **Consentement** : Case à cocher obligatoire
3. **Transparence** : Expliquez clairement ce que vous faites des données
4. **Sécurité** : Utilisez HTTPS, stockage Europe
5. **Droit d'accès** : Répondez aux demandes sous 30 jours

### Outils conformes RGPD (à utiliser)

✅ **Google Workspace** (Sheets, Docs, Slides) : Conforme RGPD
✅ **Stripe** : Conforme RGPD, données UE
✅ **Make.com** : Conforme RGPD
✅ **Mailchimp** : Conforme RGPD (option UE)

❌ **Hébergeurs US sans Privacy Shield** : À éviter

---

## 📞 RESSOURCES UTILES

### Gratuit

- **CNIL** : https://www.cnil.fr (RGPD)
- **INPI** : https://www.inpi.fr (Marques)
- **URSSAF Auto-entrepreneur** : https://www.autoentrepreneur.urssaf.fr

### Payant (mais abordable)

- **LegalPlace** : CGV/CGU/Contrats (50-100€)
- **Rocket Lawyer** : Templates juridiques (EN)
- **Avocat** : Consultation 1h (100-200€)

### Communautés

- **r/entrepreneur** (Reddit) : Conseils juridiques généraux
- **Facebook "Entrepreneurs France"**

---

## ⚠️ ERREURS À ÉVITER

❌ **Ne pas avoir de mentions légales** → Amende 1 500€
❌ **Stocker des données élèves nominatives** → RGPD violation grave
❌ **Copier-coller des CGV trouvées sur Google** → Peut ne pas être adapté
❌ **Ne pas demander le consentement email** → RGPD violation
❌ **Facturer sans créer de structure** → Travail dissimulé

---

## 🎯 MON CONSEIL

**En phase de validation (mois 1-2)** :
→ Mentions légales + Politique confidentialité + Case RGPD
→ **C'est suffisant**

**En lancement commercial (mois 3+)** :
→ Ajouter CGV + Créer micro-entreprise

**En croissance (an 2+)** :
→ SASU + Expert-comptable + Assurance

**Ne bloquez pas sur le juridique.**

Lancez avec le minimum, améliorez au fur et à mesure.

---

## ✅ CHECKLIST ULTRA-RAPIDE (1h)

**AUJOURD'HUI, fais ça** :

1. [ ] Créer page "Mentions légales" (copier-coller template ci-dessus)
2. [ ] Créer page "Politique de confidentialité" (copier-coller template)
3. [ ] Ajouter case RGPD dans formulaire Google Forms
4. [ ] Ajouter liens footer landing page

**DEMAIN, fais ça** :

5. [ ] Créer micro-entreprise (si tu comptes facturer)

**LA SEMAINE PROCHAINE** :

6. [ ] Créer CGV (si lancement commercial)

---

**Voilà, t'es couvert légalement. Go lancer ! 🚀**
