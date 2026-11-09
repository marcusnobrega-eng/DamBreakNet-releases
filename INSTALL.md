# Installing DamBreakNet for QGIS

DamBreakNet makes rapid maps of the maximum flood after a dam break, for dams in
Brazil. It runs three methods on the same inputs: DamBreakNet (a neural network,
three trained seeds), and the LNEC/ANA and HAND methods. It is for non-commercial
use only (see LICENSE.md). The maps are rapid estimates, not a replacement for a 2D
hydrodynamic study.

Setup takes about 15 minutes, most of it waiting. There are three steps.

## 0. Download

From the latest release on this page, download `DamBreakNet_v0.2.0.zip`.

## 1. Install QGIS

QGIS 3.22 or later, from https://qgis.org. This test version was checked with QGIS
3.44 on macOS; Windows and Linux are not tested yet.

## 2. Install the plugin

1. In QGIS, open Plugins, then Manage and Install Plugins, then Install from ZIP.
2. Choose `DamBreakNet_v0.2.0.zip` and click Install Plugin.
3. Click the red DamBreakNet icon in the toolbar. The panel opens on the right.

## 3. Set up the engine

The methods run in their own Python, so they do not touch the Python inside QGIS.

1. In the panel, click **Set up the engine** and then Yes.
2. Wait about 10 minutes. The plugin downloads micromamba (about 10 MB) and the
   engine's packages (about 1 GB, from conda-forge) and builds the engine in the
   folder `.dambreaknet` of your home folder. The progress bar and the Log tab show
   what it is doing.

You do this once. Nothing else needs to be installed.

## First run

Type `pirapama` in step 1, press Enter and click Run. The maps appear in the Layers
panel after about 15 seconds. Pirapama and Nilo Coelho come prepared with the plugin.

## New dams: sign in to Earth Engine

Every other dam needs land use from MapBiomas, which the plugin reads through Google
Earth Engine. Earth Engine is free for non-commercial use.

1. Register a project at https://code.earthengine.google.com/register and note its
   project ID.
2. In the panel's Settings tab, enter the project ID under Earth Engine project.
3. Click **Sign in to Earth Engine**. A browser window opens; sign in with the same
   Google account. The panel then checks that the project works.

A new dam takes 2 to 5 minutes the first time, mostly to download its terrain. The
first new dam also downloads the global OpenLandMap soil file once (437 MB) into the
`cache` folder of the Prepared data folder. For a dam that is not in SNISB, choose
"My own dam" in step 1, draw the crest on the map and type the height, volume and
material.

## Your own Python (optional)

If you prefer to manage the Python yourself, create it from `environment.yml` (conda)
or `requirements.txt` (pip) and enter its path in the Settings tab, under Python:

```bash
conda env create -f environment.yml
```

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

The Log tab has the full output of every step. Please send its last 30 lines with
your operating system and QGIS version.

## Removing it

Uninstall the plugin in Manage and Install Plugins, and delete the folder
`.dambreaknet` in your home folder (the engine) and, if you wish, `DamBreakNet_SNISB`
in Documents (the prepared dams).
