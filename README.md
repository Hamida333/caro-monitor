# Monitoring Carotidien Piézoélectrique

Simulateur de monitoring continu 12 minutes par capteurs piézoélectriques AlN/Kapton positionnés sur la carotide primitive.

## Protocole simulé
- **0–3 min** : Repos assis
- **3–12 min** : Montée de 4 étages (effort progressif)

## Modèles
- **Modèle 1** : 1 capteur — PAS/PAD continues, FC, onde de pouls, Stiffness Index, Reflection Index
- **Modèle 2** : 2 capteurs (D = 50 mm) — PTT, VOP locale, Vsys, Index de perméabilité composite (IP = α·RA + β·RS), dépistage sténose carotidienne selon critères NASCET

## Déploiement Vercel (méthode 1 — interface web)

1. Créer un compte sur [vercel.com](https://vercel.com)
2. Aller sur [vercel.com/new](https://vercel.com/new)
3. Importer ce dépôt GitHub
4. Laisser les paramètres par défaut → **Deploy**

## Déploiement Vercel (méthode 2 — CLI)

```bash
npm install -g vercel
vercel login
vercel --prod
```

## Déploiement GitHub Pages

1. Aller dans **Settings → Pages**
2. Source : `main` branch, dossier `/public`
3. Enregistrer → URL disponible en quelques secondes

## Structure du projet

```
├── public/
│   └── index.html       # Application complète (single-file)
├── vercel.json          # Configuration Vercel
└── README.md
```

## Paramètres calibration
- PAS / PAD / FC au repos
- Taille (pour calcul Stiffness Index)
- Diamètre artériel estimé (modèle 2)
- Pondérations α/β libres (IP composite) — à optimiser sur données Doppler de référence

## Critères d'alerte
| Paramètre | Seuil avertissement | Seuil alarme |
|-----------|--------------------|----|
| PAS | — | > 145 mmHg |
| PAD | — | > 95 mmHg |
| FC | — | > 140 bpm |
| Vsys | ≥ 1.25 m/s (sténose ≥50%) | ≥ 2.30 m/s (sténose ≥70%) |
| IP composite | 0.60–0.85 (limite) | < 0.60 (suspicion sténose) |

## Références
- Critères NASCET (North American Symptomatic Carotid Endarterectomy Trial)
- Bernoulli simplifié : ΔP = ½ρv², ρ = 1060 kg/m³
- AAMI : MAE < 5 mmHg, STD < 8 mmHg
