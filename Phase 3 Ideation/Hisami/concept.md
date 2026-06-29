# Concept retenu — VéloScan
> Donner une seconde vie au FACOM SCANDIAG® pour la maintenance des vélos en libre-service

---

## Contexte historique

Face à la raréfaction des ressources et à la pression économique, l'industrie a dû repenser ses méthodes de production en éliminant radicalement le gaspillage.

C'est dans cet esprit que nous proposons de donner une seconde vie au FACOM SCANDIAG® : transformer un produit voué au rebut en outil de diagnostic portable pour la maintenance des vélos en libre-service — Vélib, trottinettes, flottes urbaines.

---

## Description

Outil portable de diagnostic vélo. Un agent de maintenance pointe le SCANDIAG vers un vélo — la caméra détecte les fissures et déformations du cadre, le laser mesure l'usure des freins et l'épaisseur des pneus, le STM32 analyse et envoie le résultat en temps réel via Bluetooth vers l'application de gestion de flotte.

> *Un produit voué au rebut qui prolonge la vie des vélos et protège les usagers.*

---

## Problématique / enjeux RSE adressés

- **Sécurité des usagers** — détecter les défauts avant qu'un accident se produise
- **Prolonger la durée de vie des vélos** — moins de remplacement = moins de déchets
- **Réemploi à ~95%** — boîtier, bouton, ergonomie, tous les composants conservés
- **Double impact RSE** — le SCANDIAG est réemployé ET prolonge la vie des vélos inspectés
- **Mobilité douce** — soutenir le développement du vélo en ville ✅

---

## Principe de fonctionnement

```
Agent de maintenance tient le SCANDIAG
        ↓
Pointe vers le vélo à inspecter
        ↓
Appuie sur le bouton original
        ↓
Caméra détecte fissures / déformations du cadre
Laser mesure usure freins / épaisseur pneus
        ↓
STM32 analyse
        ↓
Résultat → Bluetooth → App gestion de flotte
        ↓
LED RGB → 🟢 vert = vélo OK / 🔴 rouge = mise en maintenance
Buzzer  → alerte sonore si défaut critique
```

---

## Contexte d'utilisation — Vélib / location de vélos 🚲

| Élément inspecté | Caméra | Laser |
|---|---|---|
| Cadre | Fissures, déformations | — |
| Freins | Présence des patins | Usure / épaisseur |
| Pneus | Déchirures, déformations | Épaisseur de la gomme |
| Guidon | Déformation, alignement | Distance / angle |
| Selle | État général | Hauteur |

**Flux de travail agent :**
1. Scan rapide du vélo → 10 secondes
2. Résultat immédiat sur smartphone
3. Vélo remis en service ✅ ou signalé en maintenance 🔴
4. Données envoyées automatiquement au centre de gestion

---

## Fonctionnalités majeures utilisées

| Composant | Rôle dans le concept |
|---|---|
| Caméra OV9712 | Détection visuelle des défauts cadre / pneus / freins |
| Laser classe 3R | Mesure d'usure et d'épaisseur |
| STM32F429NIH6 | Traitement embarqué et analyse |
| WT12-A Bluetooth | Transmission vers app gestion de flotte |
| Batterie EEMB LP602248 | Autonomie totale sur le terrain |
| LED RGB | Signal visuel vert / rouge |
| Buzzer | Alerte sonore si défaut critique |
| Bouton original | Déclenchement du scan |
| Boîtier original | Ergonomie à la main conservée |

---

## Installation physique

Le SCANDIAG est utilisé **à la main** — boîtier, bouton et ergonomie d'origine entièrement conservés. Taux de réemploi maximal (~95%).

**Avantages :**
- Rien n'est jeté ✅
- Portable sur tout le terrain urbain ✅
- Pas d'installation fixe coûteuse ✅
- Zéro formation — même geste intuitif ✅

---

## Ajouts nécessaires

| Ajout | Rôle |
|---|---|
| Modèle IA vélo (OpenCV / TF Lite) | Détection défauts spécifiques aux vélos |
| API Backend (Node.js / Python) | Centralisation des données de flotte |
| App mobile (React Native) | Interface agent + gestion de flotte temps réel |

---

## Notation

| Critère | Note |
|---|---|
| Valeur perçue | 9/10 |
| Difficulté technique | 7/10 |
| Taux de réemploi | ~95% |
| Pertinence RSE | ⭐⭐⭐ |

---

*Concept VéloScan — FACOM SCANDIAG® · Concours National Informatique Ynov*