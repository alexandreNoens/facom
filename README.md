

# Livrable final à FACOM

L'ensemble du travail des équipes est consolidé en un dossier unique transmis à la Direction RSE de FACOM comme proposition officielle de seconde vie pour le produit SCANDIAG®.

Contenu du dossier équipe :
- Membres de l'équipe (noms, classe, campus (préciser Ville Ynov Campus))
- Datasheets des composants clés
- Schéma fonctionnel du produit
- Descriptifs des idées de réemploi avec notation
- Concept retenu et justification
- Archive du ou des programmes développés (firmware)
- Documentation des fonctions développées

# FACOM SCANDIAG® — README Composants
> Référence : DX.TSCANPB · Concours National Informatique Ynov × FACOM  
> Document de référence — Rétro-ingénierie & Réemploi

---

## 1. Présentation du produit

| Paramètre | Valeur |
|---|---|
| Nom | FACOM SCANDIAG® |
| Référence | DX.TSCANPB |
| Usage d'origine | Diagnostic rapide d'usure des disques de frein et des pneus |
| Technologie | Laser + caméra combinés |
| Avantage clé | Inspection sans démonter les roues |
| Statut | Produit discontinué — stock immobilisé |
| Logiciel fourni | Application intuitive (disques / pneus / contrôle rapide) |
| Rapport | Imprimable / email / SMS |

---

## 2. Spécifications techniques

| Paramètre | Valeur |
|---|---|
| Type de batterie | Li-Ion |
| Capacité batterie | 0,620 Ah |
| Tension batterie | 3,7 VCC |
| Autonomie | 500 mesures (environ 60 véhicules) |
| Alimentation externe | 100–240 VCA |
| Connecteur alimentation | USB Mini-B (5V / 0,5A) |
| Laser | Classe 3R |
| Communication sans fil | Module Bluetooth® intégré |
| Température de fonctionnement | 0 à 40 °C |
| Température de stockage | -20 à 60 °C |
| Conformité | CE / Directive 2014/53/UE / RoHS / EMC |
| Dimensions boîtier | 330 x 215 x 60 mm |

---

## 3. Composants identifiés

### 3.1 Trouvés lors du démontage

| Référence | Type | Rôle | Fabricant | Potentiel réemploi |
|---|---|---|---|---|
| IS42S16400J-6BLI | SDRAM 64Mbit | Mémoire de travail du MCU | ISSI | ⭐⭐⭐ Très élevé |
| WT12-A | Module Bluetooth 2.1+EDR | Communication sans fil | Bluegiga / Silicon Labs | ⭐⭐⭐ Très élevé |
| RB151 | Diode redresseuse | Protection alimentation | Formosa | ⭐ Moyen |

### 3.2 À identifier (liste de référence)

| Composant recherché | Référence trouvée | Rôle | Statut |
|---|---|---|---|
| MCU / SoC | STM32F429NIH6 — ARM Cortex-M4, 180MHz, BGA216 | Traitement principal | ✅ Identifié |
| Caméra CMOS | OV9712 (JAL-KM1-OV9712 V4.0) — 1Mpx, 30fps | Capture image | ✅ Identifié |
| Laser + driver | Classe 3R, vert 510–530nm, ≤5mW — driver à vérifier | Mesure d'usure par projection | ⚠️ Driver à confirmer |
| Batterie Li-Po | EEMB LP602248 — 3,7V / 620mAh / 2,3Wh, JST 2 broches | Alimentation portable | ✅ Identifié |
| Module Bluetooth | WT12-A (Silicon Labs / Bluegiga) — BT Classic 2.1+EDR | Communication sans fil UART | ✅ Identifié |
| Mémoire SDRAM | IS42S16400J-6BLI (ISSI) — 64Mbit, 4Mx16, bus FMC | Mémoire de travail / tampon image | ✅ Identifié |
| Mémoire flash | Micron — marquage 9DA15 / RB151 (FBGA à décoder) | Stockage firmware / calibration | ⚠️ Référence à décoder |
| Diode redresseuse | RB151 (Formosa) | Protection alimentation | ✅ Identifié |
| Convertisseur DC-DC | 2 inductances visibles — références à vérifier | Génère rail 3,3V | ⚠️ À confirmer |
| Régulateur de puissance | À vérifier | Stabilisation tensions caméra / laser | ⚠️ À confirmer |
| Connecteur USB Mini-B | Confirmé — USB OTG vers MCU à vérifier | Charge + données | ✅ Identifié |
| Bouton poussoir | Bouton multifonction unique — référence SMD à confirmer | Interface utilisateur | ✅ Identifié (visuel) |
| LED RGB | Confirmée — bleu=BT / vert=charge / rouge=batterie faible | Indicateur de statut | ✅ Identifié |
| Buzzer | Confirmé | Bips de confirmation sonore | ✅ Identifié |
---

## 4. Schéma d'alimentation (restitué)

```
Batterie Li-Ion (3,7V)
        │
        ▼
    [RB151]
    Diode de protection
    (empêche le courant de remonter)
        │
        ▼
  [DC-DC Convertisseur]
    Conversion tension
        │
        ├──► 3,3V ──► MCU / SoC
        │            WT12-A (Bluetooth)
        │            IS42S16400J (SDRAM)
        │
        └──► 5V  ──► Caméra CMOS
                     Laser + driver
```

---

## 5. Potentiel de réemploi global

| Composant | Usage dans le réemploi | Priorité | Disponibilité |
|---|---|---|---|
| Caméra CMOS | Vision par ordinateur / détection défauts | 🔴 Très haute | ⚠️ À identifier |
| Laser classe 3R | Télémétrie / mesure dimensionnelle | 🔴 Très haute | ⚠️ À identifier |
| MCU / SoC | Traitement embarqué / logique de détection | 🔴 Très haute | ⚠️ À identifier |
| WT12-A (BT) | Transmission données vers dashboard / smartphone | 🟠 Haute | ✅ Identifié |
| IS42S16400J (SDRAM) | Stockage temporaire images / mesures | 🟠 Haute | ✅ Identifié |
| Batterie Li-Ion | Alimentation portable du système | 🟡 Moyenne | ✅ Identifié (doc) |
| RB151 (diode) | Protection circuits dans nouveau projet | 🟢 Faible | ✅ Identifié |

---

## 6. Concept de réemploi retenu — Andon Numérique

> Inspiré du Toyota Production System (Kaizen, Poka-Yoke, Andon)

**Station de contrôle qualité industrielle** utilisant caméra + laser + Bluetooth pour détecter les défauts sur ligne de production en temps réel.

| Critère | Valeur |
|---|---|
| Valeur perçue | 9/10 |
| Difficulté technique | 7/10 |
| Taux de réemploi | ~90% |
| Enjeu RSE | Zéro déchet industriel |

### Architecture système

```
[Pièce à inspecter]
        │
        ▼
[Caméra CMOS + Laser]  ←── SCANDIAG réemployé
        │
        ▼
[MCU / SoC]  ──► traitement embarqué
        │
        ▼
[WT12-A Bluetooth]
        │
        ▼
[Passerelle BT — Raspberry Pi / PC]
        │
        ├──► [API Backend] ──► [Dashboard Web temps réel]
        │
        └──► [Andon LED] ──► 🟢 OK / 🔴 NOK + alerte sonore
```

---

## 7. Consignes de sécurité

> ⚠️ **Laser classe 3R** : ne jamais pointer vers les yeux — porter des lunettes de protection  
> ⚠️ **Batterie Li-Ion** : éviter court-circuit et surchauffe — arrêter si gonflement  
> ⚠️ **Composants démontés** : tout reste dans la zone de travail (exigence RSE)  
> ⚠️ **Documentation** : photos + notes en continu à chaque étape

---

*README Composants — FACOM SCANDIAG® DX.TSCANPB · Concours National Informatique Ynov*

