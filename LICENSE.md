# Licences

Copyright © 2026 Marcus Nóbrega Gomes Júnior.

**Status: proposed, pending review by Stanford's Office of Technology Licensing.**
The full licence texts will be added to this package before it is distributed.

DamBreakNet is for non-commercial use. The package has three parts, under three
licences:

| Part | Files | Licence |
|---|---|---|
| QGIS panel | `*.py` in this folder, `icons/`, `metadata.txt` | GPL-2.0-or-later (it uses the QGIS API) |
| Engine | `engine/` (runners, inference, preparation, LNEC/ANA and HAND methods) | PolyForm Noncommercial License 1.0.0 |
| Trained weights | `checkpoints/` | CC BY-NC 4.0 |

The engine runs in a separate Python process from the panel.

- GPL-2.0-or-later: https://spdx.org/licenses/GPL-2.0-or-later.html
- PolyForm Noncommercial 1.0.0: https://polyformproject.org/licenses/noncommercial/1.0.0/
- CC BY-NC 4.0: https://creativecommons.org/licenses/by-nc/4.0/

The dam list (`data/snisb_dams.csv`) comes from ANA's public SNISB inventory. The
data the preparation downloads keep their own licences; see INSTALL.md.

Please cite the DamBreakNet paper when you use the maps or the weights.
