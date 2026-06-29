# Index Datasheets (rendu leger)

Objectif: pour chaque dossier composant, conserver un PDF archive + une synthese courte dans `SYNTHESE.md`.

## Couverture actuelle

- Battery
  - PDF: `LiPo-Battery-LP602248.pdf`
  - Synthese: `Battery/SYNTHESE.md`
  - Source officielle: EEMB (URL exacte a tracer)
- Camera
  - PDF: `LI-OV9712-USB-M8_datasheet.pdf`
  - Synthese: `Camera/SYNTHESE.md`
  - Source officielle: OmniVision (acces public parfois limite)
- Driver Laser
  - PDF: `IEC-60825-1-2014.pdf` (norme securite)
  - Synthese: `Driver Laser/SYNTHESE.md`
  - Source officielle composant: manquante (reference driver non lue)
- MCU
  - PDF: `stm32f427ag.pdf`
  - Synthese: `MCU/SYNTHESE.md`
  - Source officielle attendue: ST, reference exacte STM32F429NIH6
- Module Bluetooth
  - PDF: `WT12 Data Sheet - WT12-DataSheet.pdf`
  - Synthese: `Module Bluetooth/SYNTHESE.md`
  - Source officielle: Silicon Labs / Bluegiga WT12
- SDRAM 64Mbit
  - PDF: `42-45S16400J.pdf`
  - Synthese: `SDRAM 64Mbit/SYNTHESE.md`
  - Source officielle: ISSI

## TODO prioritaires

1. Remplacer le PDF MCU par la bonne reference couvrant explicitement STM32F429NIH6.
2. Decoder le marquage flash Micron (`9DA15`/`RB151`) puis ajouter le PDF constructeur.
3. Identifier la reference du driver laser et archiver sa datasheet.
4. Ajouter les URLs officielles exactes et date de recuperation dans chaque `SYNTHESE.md`.
