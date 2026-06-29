# Projet RéProfil : une seconde vie pour le SCANDIAG

> Nom de travail, à valider en équipe. Concours national RSE FACOM, Ynov Campus.

---

## 1. Le projet en une phrase

Donner une seconde vie à l'électronique du FACOM SCANDIAG, aujourd'hui arrêté et immobilisé en stock, en la transformant en **profilomètre laser** : un instrument portable qui mesure le relief et les cotes d'une pièce grâce à son laser et sa caméra, et qui sert aussi bien au contrôle qu'à la formation.

---

## 2. Le contexte et l'enjeu RSE

Le SCANDIAG était un analyseur d'usure de disques de freins et de pneus, performant mais commercialement arrêté. Il reste un stock conséquent, et FACOM refuse de le mettre au rebut. Or cette électronique a de la valeur : un microcontrôleur STM32 puissant, une caméra, un laser de mesure, un module Bluetooth, une batterie rechargeable. La jeter serait un gaspillage.

Notre projet réemploie cette électronique au lieu de la détruire. Il prolonge la vie de composants de qualité, évite le gaspillage industriel, et s'inscrit dans la démarche RSE de FACOM, qui vise une réduction de son impact environnemental. Il touche aussi un autre pilier de la marque : la formation des jeunes, FACOM étant partenaire des WorldSkills et équipant les apprentis des filières mécaniques.

---

## 3. Le concept

Le SCANDIAG mesurait déjà l'usure d'un disque par triangulation laser. Nous gardons exactement cette technique, mais nous l'ouvrons à la mesure de pièces en général.

Le principe est simple : le laser projette une ligne sur la pièce. Là où la surface est plate, la ligne reste droite. Là où il y a un creux, une marche ou une usure, la ligne suit la forme et plonge dedans. La caméra, qui regarde sous un léger angle, voit cette déformation. La forme de la ligne correspond alors au profil exact de la pièce, que le logiciel convertit en millimètres.

En déplaçant la pièce et en empilant plusieurs profils, on peut même reconstruire une représentation 3D du relief.

---

## 4. Cas d'usage

C'est le cœur de l'intérêt du projet. Le même outil couvre plusieurs besoins concrets, du plus fidèle au produit d'origine au plus large.

### Dans l'automobile et l'atelier, le cœur de métier FACOM

**Mesure d'usure des freins.** Reprendre l'usage originel : contrôler l'épaisseur restante d'un disque ou d'une plaquette de frein, sans démonter, et produire un relevé clair à montrer au client pour justifier une intervention. C'est l'usage que le SCANDIAG faisait déjà, donc le réemploi est parfaitement cohérent.

**Contrôle de l'usure des pneus.** Mesurer la profondeur de sculpture restante sur la bande de roulement, pour vérifier qu'un pneu est encore conforme.

**Usure de pièces mécaniques.** Au-delà des freins, mesurer l'usure d'un arbre, d'une portée, d'une came, d'une gorge : partout où une cote doit rester dans une tolérance, l'outil donne le profil réel.

### Dans l'industrie et la maintenance

**Contrôle dimensionnel en réception ou en production.** Vérifier qu'une pièce respecte sa cote : profondeur d'une rainure, hauteur d'une marche, largeur d'une gorge. L'outil compare le profil mesuré à la valeur attendue et indique si la pièce est bonne ou hors tolérance.

**Inspection de cordons de soudure.** Relever le profil d'un cordon pour vérifier qu'il n'est ni trop creux ni trop bombé, un contrôle classique en maintenance industrielle.

**Détection de défauts de surface.** Repérer une rayure profonde, un impact, une déformation, en lisant l'irrégularité du profil.

### Dans la formation, l'ADN WorldSkills de FACOM

**Outil pédagogique pour apprentis.** Donner aux étudiants des filières mécaniques un instrument moderne pour comprendre concrètement la métrologie : voir la cote se dessiner à l'écran, comprendre ce qu'est une mesure de profil, manipuler un appareil de mesure issu du réemploi. Un outil qui enseigne et qui incarne la RSE en même temps.

### Dans la réparation et l'économie circulaire

**Numérisation de petites pièces.** Relever le profil ou la forme 3D d'une pièce pour la documenter, voire la reproduire par impression 3D quand elle n'est plus disponible à la vente. Réparer plutôt que remplacer, encore une fois dans l'esprit RSE.

### Au-delà de la mécanique : perspectives d'ouverture

Le principe est universel : dès qu'on a besoin de connaître la forme, le relief, la profondeur ou l'épaisseur de quelque chose sans le toucher, l'outil a un usage. Au-delà du cœur de métier, le concept pourrait servir dans le quotidien et dans d'autres secteurs.

**Maison et bricolage.** Vérifier la planéité d'une surface avant de poser un carrelage ou un plan de travail, mesurer la profondeur d'une rainure, contrôler un montage.

**Artisanat et fabrication.** Vérifier la régularité d'une moulure en menuiserie, la profondeur d'un motif gravé, l'épaisseur d'une paroi en céramique. Le laser lit le relief là où l'œil se trompe.

**Alimentaire et agriculture.** Calibrer un fruit ou un légume, trier selon la taille, contrôler la régularité d'une découpe. Un usage déjà répandu en tri automatique.

**Santé et bien-être.** Relever le profil d'une voûte plantaire en podologie, mesurer une zone du corps pour un appareillage sur mesure, ou suivre l'évolution d'une plaie par sa profondeur.

**Patrimoine et culture.** Numériser le relief d'une pièce de monnaie, d'un bas-relief ou d'une inscription gravée pour l'archiver sans la manipuler.

Le fil rouge : partout où l'on dit aujourd'hui « ça a l'air plat » ou « ça semble bon », le profilomètre transforme une impression en mesure chiffrée, sans contact et rapidement. Ces pistes restent des perspectives; le cœur du projet demeure la mesure de pièces dans l'univers atelier.

---

## 5. Les composants réutilisés

| Composant | Réutilisé pour |
|---|---|
| Ligne laser verte (classe 3R) | Projeter la ligne de mesure |
| Caméra OV9712 (1 Mpx) | Capturer la déformation de la ligne |
| STM32F429 (Cortex-M4, DCMI) | Acquérir l'image et extraire le profil |
| Module Bluetooth WT12 ou USB | Transmettre le profil au PC |
| Batterie Li-Po rechargeable | Autonomie portable |
| Bouton, LED RGB, buzzer | Déclencher la mesure, indiquer l'état |

Taux de réemploi estimé : environ 85 %. Presque toute l'électronique est conservée.

---

## 6. La preuve de concept et la faisabilité

Le POC est découpé en paliers, pour garantir une démonstration quoi qu'il arrive, puis monter aussi haut que le temps le permet.

- **Palier garanti** : capturer une tranche laser sur une pièce et l'afficher en millimètres sur un PC. Cela prouve toute la chaîne de mesure.
- **Paliers suivants** : reprendre le contrôle du STM32, sortir une image de la caméra, faire l'extraction du profil directement sur la puce et l'envoyer en Bluetooth.
- **Vision d'industrialisation** : scan 3D complet du relief, comparaison automatique à une cote de référence, interface pédagogique.

À 4 personnes sur 7h, le défi principal est la mise en route de la caméra sur le microcontrôleur. La stratégie en paliers permet de sécuriser le résultat sans dépendre d'un seul point bloquant.

---

## 7. Pourquoi ce projet parle à FACOM

Il reste dans leur univers : l'atelier, la pièce, le geste de mesure, pas le relevé de bâtiment. Il prolonge l'usage d'origine du produit au lieu de le dénaturer. Il sert leur démarche RSE en évitant la mise au rebut d'une électronique de qualité. Et il touche leur engagement pour la formation des jeunes, en proposant un outil pédagogique concret pour les apprentis mécaniciens. Faisable, fidèle au métier, et responsable.
