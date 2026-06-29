# Projet Réemploi SCANDIAG : Fiche technique du matériel

Rétro-ingénierie et réemploi en seconde vie du **FACOM DX.TSCAN** (nom commercial *SCANDIAG*, réf `DX.TSCAN-1`), un analyseur de disques de freins et de pneus de Stanley Black & Decker. Ce document recense chaque composant clé trouvé lors du démontage : son rôle, sa référence, et son potentiel de réemploi.

Concours national RSE FACOM, Ynov Campus.

> Légende des statuts : **[confirmé]** référence lue directement sur la puce, **[à vérifier]** demande une confirmation visuelle ou un décodage de marquage.

---

## 1. Ce que faisait l'appareil d'origine

Un instrument portatif posé sur un disque de frein ou un pneu. Un **laser vert** mesure l'usure, une **caméra 1 Mpx** capture la surface, et les résultats sont envoyés en **Bluetooth** à un PC Windows exécutant le logiciel SCANDIAG, qui produit un rapport d'usure.

À retenir pour le réemploi : la carte est une plateforme embarquée compacte et autonome sur batterie, construite autour d'un MCU STM32 puissant, d'une caméra et d'un lien Bluetooth. Presque tout est réutilisable.

---

## 2. Schéma fonctionnel du système

Version détaillée: voir [SCHEMA_PRINCIPE_FONCTIONNEL.md](SCHEMA_PRINCIPE_FONCTIONNEL.md).

Schéma de principe (résumé):

```
USB Mini-B 5V ----+
                   +--> [Chargeur + DC-DC/regulateurs] --> 3,3V logique --> STM32F429NIH6
Li-Po 3,7V -------+

STM32F429NIH6 <--> SDRAM IS42S16400J (FMC)
STM32F429NIH6 <--> Camera OV9712 (DCMI + I2C config)
STM32F429NIH6 --> Driver laser --> Diode laser verte (<= 5 mW)
STM32F429NIH6 <--> WT12-A Bluetooth (UART)
STM32F429NIH6 <--> UI locale (bouton, LED RGB, buzzer)
STM32F429NIH6 --> Option ecran/IHM (LTDC RGB, SPI, I2C selon extension)

Connecteurs externes: USB Mini-B, JST batterie, pads SWD.
```

Caractéristiques clés (préliminaires):
- Batterie: Li-Po 3,7 V nominal, 620 mAh.
- Niveaux logiques carte: 3,3 V majoritaires.
- Interfaces principales: UART, I2C, SPI (potentiel), DCMI caméra, FMC SDRAM, USB OTG FS (à confirmer côté câblage D+/D-).
- Consommation système: ordre de grandeur 60 à 380 mA selon mode (veille, acquisition, BT, laser), à confirmer par mesure.

---

## 3. Inventaire des composants

### 3.1 Microcontrôleur (le cerveau)

| Champ | Valeur |
|---|---|
| Référence | **ST STM32F429NIH6** [confirmé] |
| Type | ARM Cortex-M4 avec FPU, jusqu'à 180 MHz |
| Mémoire | 2 Mo de flash interne, 256 Ko de SRAM, boîtier BGA216 |
| Périphériques clés | DCMI (interface caméra), LTDC (contrôleur écran TFT), USB OTG, UART, SPI, I2C, FMC (bus mémoire externe) |
| Rôle ici | Pilote la caméra, le laser, le module Bluetooth et l'interface; exécute la logique de mesure |
| Datasheet | Page produit ST, chercher `STM32F429NI` sur st.com |
| Valeur de réemploi | Très élevée. Entièrement documenté, toolchain gratuite (STM32CubeIDE), carte d'évaluation quasi identique existante (STM32F429 Discovery) |

Les périphériques DCMI et LTDC expliquent l'architecture de la carte : ce MCU est conçu pour gérer un capteur caméra et éventuellement un écran, donc la capture vidéo et la sortie écran sont des usages prévus, pas des bricolages.

### 3.2 Module Bluetooth

| Champ | Valeur |
|---|---|
| Référence | **Silicon Labs / Bluegiga WT12-A** [confirmé] |
| Type | Module Bluetooth Classic 2.1 + EDR, blindé, antenne intégrée |
| Interface | Piloté en UART depuis le STM32 |
| Rôle ici | Lien sans fil vers le PC hôte |
| Datasheet | Site Silicon Labs, chercher `WT12` |
| Valeur de réemploi | Bon pour un lien série classique sur Bluetooth. À noter : ce n'est PAS du BLE, donc pas de profils basse consommation; il se comporte comme un câble série sans fil |

### 3.3 SDRAM externe

| Champ | Valeur |
|---|---|
| Référence | **ISSI IS42S16400J** [confirmé] |
| Type | SDRAM 64 Mbit (4M x 16) |
| Interface | Bus FMC du STM32 |
| Rôle ici | Mémoire de travail du MCU, probablement tampon d'image pour la caméra |
| Datasheet | Site ISSI, chercher `IS42S16400J` |
| Valeur de réemploi | RAM supplémentaire disponible pour des tampons image ou un affichage |

### 3.4 Mémoire flash non volatile

| Champ | Valeur |
|---|---|
| Référence | **Micron**, marquage boîtier `9DA15` / `RB151` [à vérifier] |
| Type | Mémoire flash (décoder le marquage FBGA Micron pour obtenir la référence complète) |
| Rôle ici | Stocke le firmware, les données de calibration ou des images |
| Datasheet | Décodeur de référence FBGA Micron, puis la datasheet correspondante |
| Valeur de réemploi | Stockage persistant disponible pour vos propres usages |

> Action : utiliser le décodeur de marquage Micron pour transformer `9DA15`/`RB151` en référence réelle avant de la citer dans le dossier.

### 3.5 Caméra

| Champ | Valeur |
|---|---|
| Référence | **OmniVision OV9712** [confirmé], nappe `3AL-KM1-OV9712 V4.0` |
| Type | Capteur d'image CMOS, WXGA 1 Mpx, jusqu'à 30 fps |
| Interface | Sortie parallèle vers le DCMI du STM32 |
| Rôle ici | Capture la surface du disque ou du pneu |
| Datasheet | OmniVision, chercher `OV9712` |
| Valeur de réemploi | Élevée. Une caméra 1 Mpx fonctionnelle pilotée par une interface MCU native |

### 3.6 Laser

| Champ | Valeur |
|---|---|
| Référence | Diode laser classe 3R (lue sur l'étiquette du boîtier) [confirmé] |
| Specs | Sortie <= 5 mW, longueur d'onde 510 à 530 nm (vert), durée d'impulsion 10 ms |
| Norme | IEC 60825-1:2014 |
| Rôle ici | Mesure d'usure par projection laser |
| Valeur de réemploi | Utilisable comme source laser verte pilotable. SÉCURITÉ CRITIQUE, voir section 5 |
| Driver | Puce de pilotage à courant constant près de la diode [référence à vérifier] |

### 3.7 Batterie

| Champ | Valeur |
|---|---|
| Référence | **EEMB LP602248** [confirmé] |
| Type | Li-Po, 3,7 V, 620 mAh, 2,3 Wh |
| Connecteur | JST 2 broches |
| Rôle ici | Alimentation portable |
| Datasheet | Site EEMB, chercher `LP602248` |
| Valeur de réemploi | Source d'énergie rechargeable pour un appareil portable réemployé |

### 3.8 Gestion de l'alimentation

| Champ | Valeur |
|---|---|
| Référence | 2 inductances DC-DC visibles, régulateurs [à vérifier] |
| Rôle ici | Génère le rail 3,3 V et les tensions caméra/laser à partir de la batterie |
| Valeur de réemploi | Arbre d'alimentation existant réutilisable tel quel |

### 3.9 Interface utilisateur et connecteurs

| Élément | Notes |
|---|---|
| Connecteur USB Mini-B | Charge confirmée; lignes de données USB OTG vers le MCU [à vérifier] |
| Bouton poussoir | Bouton multifonction unique [confirmé] |
| LED RGB | Indicateur de statut : bleu = Bluetooth, vert = charge, rouge = batterie faible |
| Buzzer | Bips de confirmation sonore |

---

## 4. Accès au firmware (programmation)

Le MCU est un STM32F429, donc deux voies documentées existent. Procédure complète dans `PROCEDURE_FLASH_STM32F429.md`.

- **Voie A, bootloader USB DFU** : si D+/D- atteignent le MCU, forcer BOOT0 à l'état haut et flasher via STM32CubeProgrammer en USB. Sans soudure.
- **Voie B, SWD via ST-Link** : 4 fils (SWDIO/PA13, SWCLK/PA14, GND, référence 3V3) sur les pads de test de la carte. Lire l'ID de la puce avec `st-info --probe` ou OpenOCD pour confirmer le contrôle.

Attention à la **protection en lecture (RDP)** : le niveau 1 impose un effacement complet avant reprogrammation (firmware d'origine perdu, acceptable pour un réemploi); le niveau 2 verrouille le SWD (repli sur le réemploi des périphériques via un MCU externe).

---

## 5. Sécurité

- **Laser classe 3R, <= 5 mW, vert 510 à 530 nm** : dangereux pour l'oeil en vision directe. Protection oculaire obligatoire dès que le laser est sous tension. Jamais dirigé vers un visage.
- **Batterie Li-Po 3,7 V, 620 mAh** : aucun court-circuit, aucun perçage, aucun échauffement. Isoler immédiatement en cas de gonflement ou de chaleur.
- **Règle RSE** : aucun composant n'est jeté; tout reste dans la zone de travail.

---

## 6. Suivi des datasheets

Mini-rendus légers ajoutés dans chaque dossier `datasheets/*/SYNTHESE.md`.

| Composant | Référence | Datasheet archivée | Statut |
|---|---|:---:|---|
| MCU | STM32F429NIH6 | [x] | PDF présent, variante à corriger vers référence exacte F429NIH6 |
| Bluetooth | WT12-A | [x] | PDF présent |
| SDRAM | IS42S16400J | [x] | PDF présent |
| Flash | Micron (décoder 9DA15/RB151) | [ ] | Référence complète non décodée |
| Caméra | OV9712 | [x] | PDF présent, vérifier capteur nu vs fiche module |
| Batterie | EEMB LP602248 | [x] | PDF présent |
| Driver laser | à vérifier | [ ] | Norme IEC présente, datasheet composant manquante |

---

## 7. Structure du dépôt

```
.
├── README.md                 ce fichier
├── datasheets/               une PDF par composant clé
├── photos/                   démontage, étape par étape
├── schematics/               schémas fonctionnels
├── firmware/                 code source du POC (Conventional Commits)
└── docs/                     dossier et procédures
```
