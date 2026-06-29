# Titre du concept

Lampe-camera d'inspection pour zones etroites en reparation automobile

# Description

Le SCANDIAG est reemploye comme outil portable d'inspection visuelle pour ateliers automobiles. Le laser d'origine est retire et remplace par un eclairage LED blanc pilote, afin d'eclairer et filmer des zones difficiles d'acces (compartiment moteur, passages de roue, zones derriere faisceaux, fuites, connecteurs, corrosion, fissures visibles).

L'appareil conserve son architecture embarquee (camera + MCU + batterie + Bluetooth) et envoie les images/flux vers un poste atelier. L'operateur gagne du temps de diagnostic sans demonter systematiquement les sous-ensembles.

# Problematique / enjeux RSE ou metiers adresses

- Reduire le gaspillage materiel en donnant une seconde vie a un appareil discontinué.
- Diminuer le temps de diagnostic en atelier sur les pannes difficiles d'acces.
- Augmenter la securite d'usage en supprimant la source laser classe 3R.
- Faciliter la maintenance preventive (detection visuelle precoce de fuite, usure, corrosion).
- Valoriser une approche RSE concrete: reemploi d'un materiel existant plutot qu'achat d'un nouvel endoscope complet.

# Fonctionnalites majeures utilisees et ajouts eventuellement necessaires

Fonctionnalites reutilisees:
- Camera OV9712 pour acquisition image/video.
- MCU STM32F429 pour pilotage du systeme et logique embarquee.
- Module Bluetooth WT12-A pour liaison vers poste de maintenance.
- Batterie Li-Po 3.7V 620mAh pour usage portable.
- Interface locale (bouton, LED RGB, buzzer) pour pilotage simple.

Ajouts necessaires:
- Remplacement du laser par un module LED blanc a courant constant.
- Optique de diffusion (ou petit anneau LED) pour eclairage homogene en zone confinee.
- Ajustements firmware: mode eclairage, capture image, indicateurs d'etat.
- Eventuellement une tete optique plus compacte/deportee pour acces tres etroit.

# Notation de la valeur percue de la solution (1 a 10)

9/10

# Estimation de la difficulte technique (1 a 10)

5/10

# Taux de reemploi du produit (estimatif de 0 a 100%)

80%
