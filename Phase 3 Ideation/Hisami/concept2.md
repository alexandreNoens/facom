# Concept retenu — Gardien de Chantier (安全監視ツール)
> Inspiré de la Philosophie Toyota × FACOM SCANDIAG®

---

## Contexte historique

Après la Seconde Guerre mondiale, Toyota manquait d'argent et de ressources. Il leur était impossible de copier le modèle de production de masse américain (le fordisme). Ils ont donc développé leur propre méthode, fondée sur **l'élimination radicale du gaspillage**.

C'est dans cet esprit que nous proposons de donner une seconde vie au FACOM SCANDIAG® : transformer un produit voué au rebut en outil de sécurité sur chantier intelligent.

---

## Description

Outil portable de surveillance de sécurité sur chantier. Le technicien pointe le SCANDIAG vers un opérateur ou une zone de travail — la caméra vérifie que les équipements de protection individuelle (EPI) sont bien portés (casque, gilet, barrière) et déclenche une alerte immédiate si quelque chose manque.

---

## Problématique / enjeux RSE adressés

- **Sécurité humaine** — zéro accident sur chantier = zéro gaspillage humain
- **Réemploi à ~95%** — boîtier, bouton, ergonomie, tous les composants conservés
- **Cohérence RSE totale** — un produit voué au rebut protège des vies
- **Clients naturels de FACOM** — industrie, BTP, maintenance = même cible commerciale
- **Vraiment différent du SCANDIAG d'origine** ✅

---

## Les 3 piliers Toyota appliqués

### 1. Poka-Yoke — Prévention des erreurs
> *« Rendre l'oubli d'EPI impossible à ignorer »*

```
[Opérateur sur chantier]  →  [Caméra + Laser]  →  ✓ EPI OK    →  Travail autorisé
                              Scan automatique    ✗ EPI manquant →  Arrêt + alerte
```

- La caméra OV9712 détecte la présence / absence de casque, gilet, barrière
- Le laser mesure les distances de sécurité
- Toute anomalie déclenche immédiatement une alerte

---

### 2. Andon — Visualisation instantanée
> *« Rendre le danger visible instantanément »*

| Signal | Signification | Action |
|---|---|---|
| 🟢 Voyant vert | EPI complets | Travail autorisé |
| 🔴 Voyant rouge | EPI manquant | Arrêt + alerte sonore |
| 📊 Dashboard web | Chef de chantier alerté | Intervention immédiate |

---

### 3. Kaizen — Amélioration continue
> *« Apprendre de chaque inspection pour améliorer la sécurité »*

```
① Mesurer          ② Analyser            ③ Améliorer        ④ Vérifier
Toutes les    →   Identifier les    →   Ajuster les   →   Confirmer l'effet
données           zones / moments       procédures        et recommencer
enregistrées      à risque              de sécurité             ↑
en API                                                           │
└────────────────── Boucle d'amélioration continue ─────────────┘
```

---

## Contexte d'utilisation ciblé — Chantier BTP / Industrie

```
Chef de chantier tient le SCANDIAG
        ↓
Pointe vers un opérateur ou une zone
        ↓
Appuie sur le bouton original
        ↓
Caméra détecte les EPI (casque, gilet, barrières)
Laser vérifie les distances de sécurité
        ↓
STM32 analyse
        ↓
Résultat → Bluetooth → Dashboard web / smartphone chef
        ↓
LED RGB → 🟢 vert = OK / 🔴 rouge = EPI manquant + alerte sonore
```

---

## Fonctionnalités majeures utilisées

| Composant | Rôle dans le concept |
|---|---|
| Caméra OV9712 | Détection visuelle des EPI (casque, gilet, barrière) |
| Laser classe 3R | Vérification des distances de sécurité |
| STM32F429NIH6 | Traitement embarqué — modèle de détection IA |
| WT12-A Bluetooth | Alerte vers smartphone / dashboard chef de chantier |
| Batterie EEMB LP602248 | Autonomie terrain sans alimentation externe |
| LED RGB | Voyant vert / rouge visible immédiatement |
| Buzzer | Alerte sonore |
| Bouton original | Déclenchement du scan |
| Boîtier original | Ergonomie à la main conservée |

---

## Installation physique

Le SCANDIAG est utilisé **à la main** — boîtier, bouton et ergonomie d'origine entièrement conservés. Taux de réemploi maximal (~95%).

**Avantages :**
- Rien n'est jeté ✅
- Aucune formation nécessaire — même geste que le SCANDIAG original ✅
- Portable sur tout le chantier ✅
- Pas d'installation fixe coûteuse ✅

---

## Ajouts nécessaires

| Ajout | Rôle |
|---|---|
| Modèle IA EPI (OpenCV / TF Lite) | Détection casque, gilet, barrière |
| API Backend (Node.js / Python) | Centralisation des alertes |
| Dashboard web (Vue.js / React) | Supervision temps réel pour le chef de chantier |

---

## Notation

| Critère | Note |
|---|---|
| Valeur perçue | 9/10 |
| Difficulté technique | 7/10 |
| Taux de réemploi | ~95% |
| Pertinence RSE | ⭐⭐⭐ |

---

*Concept Gardien de Chantier — FACOM SCANDIAG® · Concours National Informatique Ynov*