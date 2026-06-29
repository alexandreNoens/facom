# Concept de réemploi — Phase 3

## VisioTri — Assistant portable de tri des matériaux par vision

### Description
Réemployer le SCANDIAG en un **outil de poche d'aide au tri et à l'identification de matériaux** pour déchèteries, ateliers de réparation, recycleries et lignes de tri associatives. L'opérateur pointe l'appareil vers un objet ou une zone ; la **caméra OV9712** capture la surface, le **STM32F429** réalise une analyse visuelle légère (couleur dominante, texture, présence de marquages/codes, contraste), et l'appareil indique instantanément une catégorie via la **LED RGB** et le **buzzer**, tout en envoyant le détail en **Bluetooth** vers une tablette qui tient le journal de tri.

Plutôt que de viser une reconnaissance « IA lourde » (écartée en V1 dès la Phase 2 pour raisons CPU/RAM), on s'appuie sur des **règles visuelles simples et configurables** : tri par couleur de bac, lecture de pictogrammes/numéros de recyclage, détection de présence d'étiquette, contrôle « plein/vide » d'un contenant. Le **laser vert** sert d'aide au pointage (viseur) pour cadrer l'objet à analyser.

Le produit est packagé : firmware de classification configurable + appli tablette de suivi/statistiques de tri. C'est un outil métier RSE concret né d'un produit RSE recyclé.

### Problématique / enjeux RSE ou métiers adressés
- **RSE bouclée** : un appareil destiné au rebut devient un outil qui **améliore le tri et le recyclage** d'autres déchets — la boucle vertueuse est lisible et marquante pour la Direction RSE de FACOM.
- **Métier** : les structures de réemploi/tri (recycleries, ESS, déchèteries) sont peu équipées en outils numériques abordables ; un assistant low-cost et nomade a une utilité directe et un faible coût d'acquisition (parc recyclé).
- **Traçabilité** : le journal Bluetooth alimente des statistiques de flux (quantités, catégories) utiles pour le reporting environnemental.

### Fonctionnalités majeures utilisées et ajouts éventuels nécessaires
Réutilisé tel quel :
- **Caméra OV9712** (DCMI + I2C/SCCB) — capture de la scène à classer.
- **STM32F429NIH6** — traitement d'image léger (histogramme couleur, seuils, motifs simples).
- **SDRAM IS42S16400J** (FMC) — tampon image pour l'analyse.
- **WT12-A Bluetooth** (UART) — envoi des résultats vers la tablette de suivi.
- **UI locale** (LED RGB = catégorie, buzzer = confirmation, bouton = déclenchement) — feedback opérateur immédiat, usage quasi identique à l'origine.
- **Laser classe 3R** — réutilisé comme **viseur de pointage** (cadrage de la zone analysée).
- **Batterie Li-Po + power tree** — usage nomade en zone de tri.

Ajouts / développements nécessaires :
- **Firmware de classification configurable** (jeux de règles visuelles par site) — livrable central.
- **Appli tablette/PC** de réception, journal et statistiques de tri (hors carte).
- **Calibration couleur / éclairage** : la classification par couleur dépend de la lumière ambiante → mode de calibration + éventuel petit éclairage LED d'appoint (ajout faible coût).
- **Sécurité laser** : usage en viseur faible puissance + interlock, protection oculaire (laser 3R).
- **Accès firmware** : confirmer le RDP du MCU et exposer les pads SWD pour le flash.

### Notation de la valeur perçue de la solution
**7 / 10** — usage RSE très lisible et différenciant, débouché réel auprès des structures de réemploi. Valeur limitée par la robustesse d'une classification « par règles » face à la diversité réelle des déchets.

### Estimation de la difficulté technique
**6 / 10** — le traitement d'image léger reste accessible au Cortex-M4, mais la **fiabilité de classification** sous éclairage variable est le vrai défi (calibration, robustesse). Accès firmware (RDP) à sécuriser. On évite volontairement l'IA lourde pour rester dans l'enveloppe CPU/RAM/énergie de la carte.

### Taux de réemploi du produit
**≈ 90 %** — caméra, MCU, SDRAM, Bluetooth, UI, batterie et power tree sont conservés ; le laser est réaffecté en viseur. Les ajouts (éclairage d'appoint, logiciels) sont mineurs côté matériel.
