# Installing DamBreakNet for QGIS

DamBreakNet makes rapid maps of the maximum flood after a dam break. It was trained
on dams in Brazil and also runs on dams elsewhere. It runs three methods on the same inputs: DamBreakNet (a neural network,
three trained seeds), and the LNEC/ANA and HAND methods. It is for non-commercial
use only (see LICENSE.md). The maps are rapid estimates, not a replacement for a 2D
hydrodynamic study.

There are three steps.

## 0. Download

From the latest release on this page, download `DamBreakNet_v1.1.0.zip`.

## 1. Install QGIS

QGIS 3.22 or later, from https://qgis.org. This version was checked with QGIS 3.44
on macOS; Windows and Linux are not tested yet.

## 2. Install the plugin

1. In QGIS, open Plugins, then Manage and Install Plugins, then Install from ZIP.
2. Choose `DamBreakNet_v1.1.0.zip` and click Install Plugin.
3. Click the red DamBreakNet icon in the toolbar. The panel opens on the right.

## 3. Set up the engine

The methods run in their own Python, so they do not touch the Python inside QGIS.

1. In the panel, click **Set up the engine** and then Yes.
2. Wait while the plugin downloads micromamba (about 10 MB) and the
   engine's packages (about 1 GB, from conda-forge) and builds the engine in
   `C:\dbn` on Windows (or `.dbn` in your user folder, if `C:\dbn` cannot be made),
   and in `.dambreaknet` in your home folder on macOS and Linux. The progress bar and
   the Log tab show what it is doing.

If the setup stops, click **Set up the engine** again. It removes the unfinished
engine and starts over.

On Windows, version 0.2.0 stopped here with "remove_all: The directory is not empty". Its folder
paths were longer than the 260 characters Windows allows. Version 1.0.0 builds the engine in
`C:\dbn` with a flat package cache, so the longest path is 209 characters. If you saw this error,
install version 1.0.0 or later and click **Set up the engine** again.

You do this once. Nothing else needs to be installed.

## First run

Type `pirapama` in step 1, press Enter and click Run. The maps appear in the Layers
panel after about 15 seconds. Pirapama and Nilo Coelho come prepared with the plugin.

## New dams: sign in to Earth Engine

Every other dam in Brazil needs land use from MapBiomas, which the plugin reads through Google
Earth Engine. Earth Engine is free for non-commercial use.

1. Register a project at https://code.earthengine.google.com/register and note its
   project ID.
2. In the panel's Settings tab, enter the project ID under Earth Engine project.
3. Click **Sign in to Earth Engine**. A browser window opens; sign in with the same
   Google account. The panel then checks that the project works.

Dams outside Brazil need no Earth Engine account for their maps: the plugin downloads
ESA WorldCover instead and warns that DamBreakNet's accuracy there is untested. The
population of the risk report still comes through Earth Engine.

A new dam took about 2 minutes in our test, most of it to download the terrain. The
first new dam also downloads the global OpenLandMap soil file once (437 MB) into the
`cache` folder of the Prepared data folder. For a dam that is not in SNISB, choose
"My own dam" in step 1, draw the crest on the map and type the height, volume and
material.

## Risk report

After the maps, step 5 gives the people in the flood, the hazard classes H1 to H6 of the
Australian flood hazard guideline (AIDR 2017, Guideline 7-3), the schools, health units,
emergency services and roads in each class, and the self-rescue zone (ZAS).

- People come from WorldPop 2020 through Earth Engine, so they need the Earth Engine
  project above, for dams in Brazil and elsewhere. Only the dam's own area is read, about
  1 MB or less, and it is saved with the dam. Without a project the report has no people,
  and the rest still works.
- Facilities and roads come from OpenStreetMap through public Overpass servers. They are
  sometimes busy; "Retry OpenStreetMap" asks again. The answer is saved with the dam.
- The ZAS length is a setting (Settings, Risk report), 10 km by default. Use the value of
  the dam's emergency plan (PAE) when you know it.
- "Export report (PDF)" writes a five-page summary in English or Portuguese (maps, tables,
  flooded facilities with coordinates, method and suggested actions) and opens it. Its
  OpenStreetMap background needs internet.
- The two demo dams come with their people and OpenStreetMap data.

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
| Land use in Brazil | MapBiomas Collection 10 (2024), through Earth Engine | CC BY 4.0 |
| Land use outside Brazil | ESA WorldCover 2021, translated to MapBiomas classes | CC BY 4.0 |
| Soil classes | OpenLandMap USDA texture classes (Zenodo 2525817) | CC BY-SA 4.0 |
| Population | WorldPop 2020 constrained, 100 m, through Earth Engine | CC BY 4.0 |
| Facilities and roads | OpenStreetMap, through the Overpass API | ODbL; © OpenStreetMap contributors |
| Dam list | SNISB, Agência Nacional de Águas e Saneamento Básico | public data; cite ANA |
| Basemap | OpenStreetMap | ODbL; © OpenStreetMap contributors |

## Limits

- Outside Brazil, the land cover is ESA WorldCover translated to MapBiomas classes, and
  DamBreakNet's accuracy there is untested. The panel warns about it.
- DamBreakNet learned from 382 SNISB dams that were 1 to 63.2 m high and held 0.5
  to 456 hm³. The panel warns when a dam lies outside this range.
- Tailings dams are refused; they need a mudflow model.

## When something fails

The Log tab has the full output of every step. Please send its last 30 lines with
your operating system and QGIS version.

## Removing it

Uninstall the plugin in Manage and Install Plugins, then delete the engine's folder
(`C:\dbn` or `.dbn` on Windows, `.dambreaknet` on macOS and Linux) and, if you wish,
`DamBreakNet_SNISB` in Documents (the prepared dams).
