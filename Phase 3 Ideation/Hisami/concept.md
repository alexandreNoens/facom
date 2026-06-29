# Concept retenu — Andon Numérique
> Inspiré de la Philosophie Toyota × FACOM SCANDIAG®

---

## Contexte historique

Après la Seconde Guerre mondiale, Toyota manquait d'argent et de ressources. Il leur était impossible de copier le modèle de production de masse américain (le fordisme). Ils ont donc développé leur propre méthode, fondée sur **l'élimination radicale du gaspillage**.

C'est dans cet esprit que nous proposons de donner une seconde vie au FACOM SCANDIAG® : transformer un produit voué au rebut en outil de production industrielle intelligent.

---

## Description

Station de contrôle qualité industrielle utilisant les composants du SCANDIAG® pour détecter les défauts sur une ligne de production en temps réel, inspirée des 3 piliers du Toyota Production System.

---

## Les 3 piliers appliqués au système

### 1. Poka-Yoke — Prévention des erreurs
> *« Rendre l'erreur impossible à ignorer »*

```
[Pièce]  →  [Caméra + Laser]  →  ✓ Conforme  →  Ligne continue
Ligne de prod.  Scan automatique  ✗ Défaut    →  Arrêt + alerte
```

- La caméra OV9712 et le laser classe 3R scannent automatiquement chaque pièce
- Le STM32F429 analyse les données en temps réel
- Toute anomalie déclenche immédiatement un arrêt

---

### 2. Andon — Visualisation instantanée
> *« Rendre les problèmes visibles instantanément »*

| Signal | Signification | Action |
|---|---|---|
| 🟢 Voyant vert | Pièce conforme | Production continue |
| 🔴 Voyant rouge | Anomalie détectée | Arrêt immédiat |
| 📊 Dashboard web | Toute l'équipe voit le problème | Intervention en temps réel |

---

### 3. Kaizen — Amélioration continue
> *« Un système qui apprend de chaque pièce inspectée »*

```
① Mesurer          ② Analyser            ③ Améliorer        ④ Vérifier
Toutes les    →   Identifier les    →   Ajuster le    →   Confirmer l'effet
données           défauts récurrents    processus         et recommencer
enregistrées                                                      ↑
en API                                                            │
└─────────────────── Boucle d'amélioration continue ─────────────┘
```

---

## Problématique / enjeux RSE adressés

- **Zéro déchet industriel** — détecter les défauts avant qu'ils ne deviennent des rebuts
- **Réemploi à 90%** — presque tous les composants du SCANDIAG sont réutilisés
- **Cohérence RSE totale** — un produit voué au rebut sert à réduire les déchets industriels
- **Réduction des coûts** — moins de pièces défectueuses = moins de gaspillage matière

---

## Fonctionnalités majeures utilisées

| Composant | Rôle dans le concept |
|---|---|
| Caméra OV9712 | Capture image de chaque pièce à inspecter |
| Laser classe 3R | Mesure dimensionnelle non-contact |
| STM32F429NIH6 | Traitement embarqué et logique de détection |
| WT12-A Bluetooth | Transmission des données vers le dashboard |
| Batterie EEMB LP602248 | Alimentation portable autonome |

---

## Contextes d'utilisation

### 1. Atelier de fabrication automobile *(contexte FACOM naturel)*
- Vérifier les pièces avant montage
- Détecter les pièces déformées ou hors tolérance
- Même environnement que le SCANDIAG d'origine

### 2. Ligne d'assemblage électronique
- Vérifier les circuits imprimés
- Détecter les soudures manquantes ou défectueuses

### 3. Contrôle réception / logistique
- Technicien reçoit une palette de pièces
- Scanne rapidement chaque pièce à la réception
- Valide ou rejette le lot

### 4. Maintenance industrielle
- Vérifier l'usure de pièces en service
- Décider si une pièce peut encore être utilisée ou doit être changée
- *(exactement comme le SCANDIAG faisait avec les freins)*

### 5. PME / artisans
- Pas les moyens d'un système automatisé coûteux
- Outil portable, simple, pas cher
- Un geste = une réponse

> **Argument clé pour FACOM** : le contexte 4 est identique à l'usage d'origine — *même geste, même environnement, nouvelle utilité.*

---

## Installation physique

Le SCANDIAG est utilisé **à la main** — le boîtier, le bouton et l'ergonomie d'origine sont entièrement conservés. Taux de réemploi maximal (~95%).

```
Opérateur tient le SCANDIAG
        ↓
Approche la pièce à inspecter
        ↓
Appuie sur le bouton original
        ↓
Caméra + Laser scannent
        ↓
STM32 analyse
        ↓
Résultat → Bluetooth → Dashboard web
        ↓
LED RGB → 🟢 vert = OK / 🔴 rouge = NOK
```

**Avantages de l'usage à la main :**
- Boîtier original réutilisé ✅
- Bouton original réutilisé ✅
- Ergonomie conservée ✅
- Aucun support / fixation supplémentaire nécessaire ✅
- Taux de réemploi ~95% ✅

---

## Ajouts nécessaires

| Ajout | Rôle |
|---|---|
| Modèle IA (OpenCV / TF Lite) | Classification des défauts |
| API Backend (Node.js / Python) | Centralisation des données |
| Dashboard web (Vue.js / React) | Visualisation temps réel — Andon numérique |
| Voyant LED RGB | Signal physique vert / rouge |

---

## Notation

| Critère | Note |
|---|---|
| Valeur perçue | 9/10 |
| Difficulté technique | 7/10 |
| Taux de réemploi | ~95% |
| Pertinence RSE | ⭐⭐⭐ |

---

*Concept Andon Numérique — FACOM SCANDIAG® · Concours National Informatique Ynov*