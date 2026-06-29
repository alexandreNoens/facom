# Schema de principe fonctionnel - FACOM DX.TSCAN

Ce document fournit une vue systeme exploitable pour le reemploi: alimentations, MCU, interfaces camera, driver laser, Bluetooth, UI/IHM et connecteurs externes.

Statuts:
- [confirme] base sur reference lue et architecture carte.
- [a verifier] necessite mesure electrique ou lecture marquage complementaire.

## 1. Vue fonctionnelle globale

```mermaid
flowchart LR
    USB[USB Mini-B 5V\ncharge + USB OTG? [a verifier]] --> PMIC[Chargeur + DC-DC + regulateurs]
    BAT[Batterie Li-Po\n3.7V nominal\n620mAh] --> PMIC

    PMIC --> R33[Rail 3.3V logique]
    PMIC --> RCAM[Rail camera 2.8V/1.8V? [a verifier]]
    PMIC --> RLAS[Rail driver laser [a verifier]]

    R33 --> MCU[STM32F429NIH6\nCortex-M4F 180MHz]
    R33 --> BT[WT12-A\nBluetooth Classic UART]
    R33 --> UI[UI: bouton, LED RGB, buzzer]

    MCU <-->|FMC 16-bit| SDRAM[IS42S16400J\nSDRAM 64Mbit]
    MCU <-->|DCMI + I2C config| CAM[OV9712\nCamera 1Mpx]
    MCU -->|GPIO/PWM/EN| LDRV[Driver laser courant constant\nref CI [a verifier]]
    LDRV --> LASER[Diode laser verte\nClasse 3R <=5mW]

    MCU <-->|UART 3.3V TTL| BT
    BT --> ANT[Antenne integree]

    MCU -->|LTDC RGB + sync| DISP[Option ecran TFT/IHM locale]
    MCU -->|GPIO/I2C/SPI| EXT[Option IHM externe\nclavier, encodeur, capteurs]

    SWD[Pads SWDIO/SWCLK/GND/3V3] --- MCU
```

## 2. Chaine d'alimentation

| Bloc | Entree | Sortie | Charge principale | Etat |
|---|---|---|---|---|
| Batterie | Li-Po 3.7V nominal (4.2V pleine charge) | VBAT | Systeme portable | [confirme] |
| USB Mini-B | 5V | Charge batterie + alim carte | Charge + eventuel USB data | [confirme]/[a verifier pour data] |
| DC-DC / regulateurs | VBAT/5V | 3.3V logique + rails specifiques | MCU, BT, RAM, camera, laser | [confirme], refs CI [a verifier] |
| Rail logique | 3.3V | Niveaux numeriques carte | MCU, WT12, IO | [confirme] |
| Rail camera | 2.8V/1.8V typiques capteur | OV9712 | Analogique + coeur camera | [a verifier par mesure] |
| Rail laser | Selon driver | Driver + diode laser | Emission laser impulsionnelle | [a verifier] |

## 3. Interfaces et niveaux logiques

| Liaison | Interface | Niveau logique attendu | Debit / frequence (ordre de grandeur) | Usage |
|---|---|---|---|---|
| MCU <-> Camera OV9712 (video) | DCMI parallele (D[7:0], PCLK, HSYNC, VSYNC) | 3.3V (ou adapte par domaine camera) | Jusqu'a 30 fps WXGA selon config | Capture image surface |
| MCU <-> Camera OV9712 (config) | I2C/SCCB | 3.3V | 100-400 kHz | Reglage capteur (expo, gain, format) |
| MCU <-> SDRAM ISSI | FMC 16-bit + signaux SDRAM | 3.3V | Horloge memoire selon timing FMC | Buffer image / RAM externe |
| MCU <-> BT WT12-A | UART | 3.3V TTL | 115200 bps a >1 Mbps selon profil | Telemetrie et commandes PC |
| MCU <-> Flash Micron | SPI/QSPI? | 3.3V (a confirmer) | 10-50 MHz typiques | Stockage firmware/donnees |
| MCU <-> Driver laser | GPIO/EN + eventuel PWM | 3.3V logique | Impulsions 10 ms typiques usage original | Pilotage emission |
| MCU <-> UI locale | GPIO + PWM | 3.3V | Faible debit | Bouton, LED RGB, buzzer |
| MCU <-> Ecran optionnel | LTDC RGB / SPI selon dalle | 3.3V (avec adaptation selon dalle) | Pixel clock selon resolution | IHM locale enrichie |
| MCU <-> USB Mini-B | USB OTG FS | D+/D- USB | 12 Mbps (FS) | Flash/maintenance/telemetrie [a verifier cablage] |
| Debug externe | SWD (ST-Link) | 3.3V ref | Horloge SWD standard | Programmation/debug |

## 4. Consommations (budget preliminaire)

Valeurs ci-dessous en ordre de grandeur pour cadrer le schema de puissance. A confirmer a l'ammperemetre sur carte.

| Mode | Blocs actifs | Courant estime |
|---|---|---|
| Veille active | MCU + UI minimale + BT inactif | 60 a 120 mA |
| Acquisition camera | MCU + camera + SDRAM | 140 a 240 mA |
| Acquisition + BT | MCU + camera + SDRAM + WT12 liaison active | 180 a 300 mA |
| Mesure complete | MCU + camera + SDRAM + BT + laser impulsionnel | 220 a 380 mA (pics possibles >400 mA) |

Approximation d'autonomie theorique (batterie 620 mAh):
- a 120 mA: ~5.2 h
- a 250 mA: ~2.5 h
- a 350 mA: ~1.8 h

Remarque: autonomie reelle inferieure (rendement convertisseurs, vieillissement batterie, duty-cycle laser/camera, temperature).

## 5. UI et possibilites IHM

UI existante [confirme]:
- 1 bouton poussoir multifonction.
- 1 LED RGB de statut.
- 1 buzzer sonore.

Extensions IHM possibles [reemploi]:
- Ecran TFT pilote via LTDC (si lignes disponibles) ou petit ecran SPI.
- IHM externe via connecteur (UART/I2C) pour boitier de test ou pupitre atelier.
- Interface de maintenance via USB OTG (si D+/D- vraiment routes au MCU).

## 6. Connecteurs externes

| Connecteur | Fonction | Signals clefs | Etat |
|---|---|---|---|
| USB Mini-B | Charge + potentielle data USB | 5V, GND, D+, D- | Charge [confirme], data [a verifier] |
| JST 2 broches batterie | Liaison batterie Li-Po | VBAT, GND | [confirme] |
| Pads test SWD | Debug et flash | SWDIO, SWCLK, GND, 3V3 ref | [confirme] |
| Antenne integree WT12 | Radio BT | RF integre module | [confirme] |

## 7. Checklist de validation terrain

1. Mesurer rails 3.3V, camera, laser en veille et en acquisition.
2. Valider niveaux logiques des bus camera et UART BT a l'oscilloscope.
3. Confirmer chemin USB D+/D- vers MCU (continuite + essai enumeration).
4. Identifier references des CI power et driver laser pour fermer les [a verifier].
5. Mettre a jour ce schema apres mesures (version v2 mesuree).
