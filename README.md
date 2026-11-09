<img src="images/logo.png" alt="DamBreakNet logo: a broken dam feeding a small neural network" width="96" align="right">

# DamBreakNet for QGIS

**From a dam on the map to its dam-break flood map, in seconds.** Name a dam, pick it on
the map or draw your own. DamBreakNet builds the terrain, land use, soil, flood domain and
breach hydrograph, then maps the maximum flood with a neural network and two established
methods side by side. Everything happens inside QGIS, on your own computer.

![Maximum flood depth below Pirapama dam, Pernambuco, Brazil, predicted by DamBreakNet and shown over OpenStreetMap](images/map_pirapama.png)

*Pirapama dam (SNISB 007866), Cabo de Santo Agostinho, Pernambuco. Maximum depth from
DamBreakNet (seed 11) over a 131.7 km² domain on a 30 m grid (146,348 cells). The three
methods ran in about 15 seconds on a laptop CPU. Map data © OpenStreetMap contributors.*

This page holds the QGIS plugin package. It does not hold the code used to build and
train the model.

## Why DamBreakNet

- **Three methods, one click.** DamBreakNet (three trained seeds), LNEC/ANA and HAND run
  on the same inputs, and maps of the same quantity share one colour scale.
- **Any SNISB dam, or your own.** Search the 28,083 dams of Brazil's SNISB inventory by
  name, town or code, or click one on the map. For any other dam, draw its crest and type
  its height, volume and material.
- **The data, found for you.** FABDEM terrain, MapBiomas land use (through Google Earth
  Engine) and OpenLandMap soil classes are downloaded and put on one grid. The flood domain
  and the breach hydrograph are built from the dam's attributes.
- **A first quality check.** Each map gets flags for fragmentation and for the share of
  the wet area connected to the dam. A triage then says *rapid map* or *check with a 2D
  model*.
- **Plain warnings.** The panel says when a dam lies outside the range DamBreakNet learned
  from, when the preparation flags a domain for review, and why a method could not run.
- **Fast.** A prepared dam runs in about 15 seconds on a laptop CPU. A new dam takes 2 to
  5 minutes the first time, mostly to download its terrain.

<p>
<img src="images/panel_find.png" alt="Step 1 of the panel: finding Pirapama by name" width="49%">
<img src="images/panel_results.png" alt="Step 4 of the panel: the flag table and the triage for Pirapama" width="49%">
</p>

## Download

Get the latest version under **[Releases](../../releases)**.

| What | File | Size |
|---|---|---|
| QGIS plugin, with the trained weights and two prepared demo dams | `DamBreakNet_v0.2.0.zip` | 32 MB |
| Python environment for the engine | `environment.yml` (conda) or `requirements.txt` (pip) | small |

You need QGIS 3.22 or later and a separate Python for the engine. New dams also need a
free Google Earth Engine project for non-commercial use. The first new dam downloads a
437 MB soil file once.

The install steps are in **[INSTALL.md](INSTALL.md)**. In short:

1. Create the engine's Python: `conda env create -f environment.yml`.
2. In QGIS: Plugins, Manage and Install Plugins, Install from ZIP, choose the zip.
3. Click the DamBreakNet icon, type `pirapama` and click Run.

## Limits

- Dams in Brazil only, because the land use comes from MapBiomas.
- DamBreakNet learned from 382 SNISB dams that were 1 to 63.2 m high and held 0.5 to 456
  hm³. Outside that range its maps are extrapolations, and the panel says so.
- These are rapid maps for one breach scenario per dam. They do not replace a 2D
  hydrodynamic study.
- This is a test version. It was checked on macOS; Windows and Linux are not tested yet.

## How to cite

Gomes Jr., M. N., et al. DamBreakNet: A Hydrograph-Conditioned Neural Model for Dam-Break
Flood Mapping. Manuscript in review, 2026. The full reference will appear here after
publication.

## Licence

For non-commercial use. The QGIS panel is under GPL-2.0-or-later, the engine under the
PolyForm Noncommercial License 1.0.0, and the trained weights under CC BY-NC 4.0 (these
licences are proposed and still under review). The data the plugin downloads keep their
own licences, listed in [INSTALL.md](INSTALL.md). See [LICENSE.md](LICENSE.md).

## Contact

Marcus Nóbrega Gomes Júnior, Stanford University, mngomes@stanford.edu.
