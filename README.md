# Concours National Informatique — FACOM × Ynov
> Réemploi RSE du produit FACOM SCANDIAG® (réf. DX.TSCANPB)

---

## Équipe

| Nom | Classe | Campus |
|---|---|---|
| Noens Alexandre| DEVFLSTK MAST1 B | Lyon Ynov |
| Adou Eddin | DEVFLSTK MAST1 B | Lyon Ynov |
| Mechta Yanis| DEVFLSTK MAST1 B | Lyon Ynov |
| Stolz Hisami | DEVFLSTK MAST1 B | Lyon Ynov |

---

## Contexte du challenge

Le produit FACOM SCANDIAG® n'est plus commercialisé mais un stock conséquent reste immobilisé. La Direction RSE de FACOM lance un défi national à l'ensemble des campus Ynov (niveaux B2→M2) : **trouver une seconde vie aux composants** afin de revaloriser les pièces et éviter le gaspillage industriel. Les meilleures propositions seront remises directement à la Direction RSE de FACOM dans le cadre d'un partenariat industriel concret.

**Format :** 7h · équipes de 4 à 6 étudiants · multi-campus en parallèle

---

## Structure du projet

```
facom/
├── archive/             # sources PDF d'origine (non modifiées)
├── datasheets/          # Phase 1 — fiches composants + synthèses
├── docs/                # Phase 1 & 2 — schémas fonctionnels, champ des possibles
├── Phase 3 Ideation/    # Phase 3 — concepts de réemploi par membre
└── README.md
```

---

## Phase 1 — Rétro-ingénierie

**Objectif :** identifier les composants clés et produire une synthèse fonctionnelle.

| Composant | Référence | Statut |
|---|---|---|
| MCU / SoC | STM32F429NIH6 — Cortex-M4, 180 MHz | ✅ Identifié |
| Caméra CMOS | OV9712 — 1 Mpx, 30 fps | ✅ Identifié |
| Bluetooth | WT12-A (Silicon Labs) — BT Classic 2.1+EDR | ✅ Identifié |
| SDRAM | IS42S16400J-6BLI — 64 Mbit | ✅ Identifié |
| Batterie | EEMB LP602248 — 3,7 V / 620 mAh | ✅ Identifié |
| Laser | Classe 3R, vert 510–530 nm, ≤ 5 mW | ⚠️ Driver à confirmer |
| Mémoire flash | Micron — marquage 9DA15 | ⚠️ Référence à décoder |
| Diode redresseuse | RB151 (Formosa) | ✅ Identifié |

**Fichiers associés :**
- [`datasheets/`](datasheets/) — datasheets et synthèses par composant
- [`docs/SCHEMA_PRINCIPE_FONCTIONNEL.md`](docs/SCHEMA_PRINCIPE_FONCTIONNEL.md) — schéma d'alimentation et interfaces
- [`docs/FICHE_TECHNIQUE.md`](docs/FICHE_TECHNIQUE.md) — spécifications complètes du produit

**Accès firmware (voies identifiées) :**
- **Voie A — USB DFU** (sans soudure) : forcer BOOT0 haut + USB Mini-B + STM32CubeProgrammer
- **Voie B — SWD** : pads SWDIO (PA13) / SWCLK (PA14) / GND / 3,3 V

> ⚠️ Vérifier le niveau RDP avant toute tentative de flash — RDP1 = effacement firmware d'origine.

---

## Phase 2 — Champ des possibles

**Objectif :** cartographier exhaustivement ce qui est réutilisable, ce qui peut être ajouté, et les limites fonctionnelles.

**Fichier associé :** [`docs/PHASE2_CHAMP_DES_POSSIBLES.md`](docs/PHASE2_CHAMP_DES_POSSIBLES.md)

Fonctions matérielles directement réutilisables :

| Fonction | Blocs impliqués | Interfaces |
|---|---|---|
| Capture image | OV9712 + STM32 DCMI + SDRAM | DCMI, I2C/SCCB, FMC |
| Projection laser | Diode laser + driver | GPIO / PWM |
| Traitement embarqué | STM32F429NIH6 | GPIO, timers, DMA |
| Liaison sans fil | WT12-A | UART TTL 3,3 V |
| Interface opérateur | Bouton + LED RGB + Buzzer | GPIO / PWM |
| Alimentation portable | Li-Po + power tree | 3,3 V, rails dérivés |

---

## Phase 3 — Idéation

**Objectif :** imaginer des concepts de réemploi, explorer largement, puis converger sur une idée.

**Notice de phase :** [`Phase 3 Ideation/notice.md`](Phase%203%20Ideation/notice.md)

### Concepts proposés par l'équipe

| Membre | Fichier | Concept | Valeur | Difficulté | Réemploi |
|---|---|---|---|---|---|
| Yanis | [`Phase 3 Ideation/Yanis/concept.md`](Phase%203%20Ideation/Yanis/concept.md) | **VisioTri** — assistant de tri des matériaux par vision | 7/10 | 6/10 | ~90% |
| Hisami | [`Phase 3 Ideation/Hisami/concept.md`](Phase%203%20Ideation/Hisami/concept.md) | **VéloScan** — diagnostic portable pour flottes de vélos en libre-service | 9/10 | 7/10 | ~95% |
| Alexandre | [`Phase 3 Ideation/Alexandre/concept.md`](Phase%203%20Ideation/Alexandre/concept.md) | **Lampe-caméra d'inspection auto** — inspection visuelle de zones étroites | 9/10 | 5/10 | ~80% |
| Eddin | [`Phase 3 Ideation/Eddin/concept.md`](Phase%203%20Ideation/Eddin/concept.md) | Concept Eddin | — | — | — |

### Concept retenu — VisioTri (Yanis)

**Justification du choix :**
VisioTri présente l'alignement RSE le plus fort et le plus lisible : un appareil destiné au rebut devient directement un outil qui améliore le tri et le recyclage d'autres déchets, formant une boucle vertueuse convaincante pour la Direction RSE de FACOM. Le concept s'appuie sur ~90 % des composants d'origine sans ajout matériel lourd, et la classification par règles visuelles (histogramme couleur, seuils) reste réaliste dans l'enveloppe CPU/RAM du STM32F429 sans nécessiter un modèle IA embarqué coûteux. Enfin, le débouché métier est concret et immédiat — les recycleries et déchèteries sont réellement sous-équipées en outils numériques nomades abordables.

---

## Consignes de sécurité

> ⚠️ **Laser classe 3R** : ne jamais pointer vers les yeux — lunettes de protection obligatoires
> ⚠️ **Batterie Li-Ion** : éviter court-circuit et surchauffe — arrêter si gonflement
> ⚠️ **Composants démontés** : tout reste dans la zone de travail (exigence RSE)
> ⚠️ **Documentation** : photos + notes en continu à chaque étape

---

## Livrable final à FACOM

- [x] Membres de l'équipe (noms, classe, campus Ynov)
- [x] Datasheets des composants clés → [`datasheets/`](datasheets/)
- [x] Schéma fonctionnel du produit → [`docs/SCHEMA_PRINCIPE_FONCTIONNEL.md`](docs/SCHEMA_PRINCIPE_FONCTIONNEL.md)
- [x] Descriptifs des idées de réemploi avec notation → [`Phase 3 Ideation/`](Phase%203%20Ideation/)
- [x] Concept retenu et justification → [`docs/CONCEPT_RETENU_VISIOTRI.md`](docs/CONCEPT_RETENU_VISIOTRI.md)
- [ ] Archive du ou des programmes développés (firmware)
- [ ] Documentation des fonctions développées

---

*Concours National Informatique Ynov × FACOM — Campus Bordeaux · 2025*
