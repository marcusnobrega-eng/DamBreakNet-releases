# Installing DamBreakNet for QGIS

DamBreakNet makes rapid maps of the maximum flood after a dam break, for dams in
Brazil. It runs three methods on the same inputs: DamBreakNet (a neural network,
three trained seeds), and the LNEC/ANA and HAND methods. It is for non-commercial
use only (see LICENSE.md). The maps are rapid estimates, not a replacement for a 2D
hydrodynamic study.

Setup takes about 20 minutes. You need four things: QGIS, a Python for the engine,
an Earth Engine project (only for new dams) and the plugin zip.

## 0. Download

From the latest release on this page, download `DamBreakNet_v0.2.0.zip`. Download
`environment.yml` (or `requirements.txt`) from the release or from the top of this page.

## 1. QGIS

QGIS 3.22 or later, on Windows, macOS or Linux. This test version was checked with
QGIS 3.44 on macOS; Windows and Linux are not tested yet.

## 2. A Python for the engine

The methods run in a separate Python, not in the one inside QGIS. Make one with
conda (recommended) or pip, using `environment.yml` or `requirements.txt`.

With conda (on Windows, in the Miniforge or Anaconda Prompt):

```bash
conda env create -f environment.yml
conda activate dambreaknet
python -c "import sys; print(sys.executable)"
```

With pip, in a Python 3.10 or later:

```bash
python3 -m pip install -r requirements.txt
```

The panel finds a conda environment named `dambreaknet` by itself. If it does not,
or if you used pip, enter the path that the last command prints in the panel's
Settings tab, under Python.

## 3. Earth Engine (only for new dams)

Two dams come prepared with the plugin (Pirapama and Nilo Coelho) and run
without this step. Every other dam needs land use from MapBiomas, which the
preparation reads through Google Earth Engine.

1. Register a project for non-commercial use at
   https://code.earthengine.google.com/register.
2. Sign in once, in the engine's Python:

   ```bash
   earthengine authenticate
   ```

3. In the panel's Settings tab, enter the project ID under Earth Engine project.

## 4. The plugin

1. In QGIS, open Plugins, then Manage and Install Plugins, then Install from ZIP.
2. Choose `DamBreakNet_v0.2.0.zip` and click Install Plugin.
3. Click the red DamBreakNet icon in the toolbar.

On first use, the panel copies the two prepared dams into
`~/Documents/DamBreakNet_SNISB` (the Prepared data folder in Settings).

## First run

Type `pirapama` in step 1, press Enter and click Run. The maps appear in the
Layers panel after about 15 seconds.

A new dam takes a few minutes the first time. The panel shows each step:

- FABDEM terrain for 30 km around the dam, about 1 to 4 minutes;
- MapBiomas land use through Earth Engine, about 10 seconds;
- the soil classes. The first new dam downloads the global OpenLandMap soil file
  once (437 MB) into the `cache` folder of the Prepared data folder.

For a dam that is not in SNISB, choose "My own dam" in step 1, draw the crest on
the map and type the height, volume and material.

## Data and their licences

The preparation downloads public data, each under its own licence:

| Data | Source | Licence |
|---|---|---|
| Terrain | FABDEM V1-2, University of Bristol | CC BY-NC-SA 4.0 |
| Land use | MapBiomas Collection 10 (2024), through Earth Engine | CC BY 4.0 |
| Soil classes | OpenLandMap USDA texture classes (Zenodo 2525817) | CC BY-SA 4.0 |
| Dam list | SNISB, Agência Nacional de Águas e Saneamento Básico | public data; cite ANA |
| Basemap | OpenStreetMap | ODbL; © OpenStreetMap contributors |

## Limits

- Dams in Brazil only, because the land use comes from MapBiomas.
- DamBreakNet learned from 382 SNISB dams that were 1 to 63.2 m high and held 0.5
  to 456 hm³. The panel warns when a dam lies outside this range.
- Tailings dams are refused; they need a mudflow model.

## When something fails

The Log tab has the full output of every step. The Guide tab explains each step of
the panel and the flags.
