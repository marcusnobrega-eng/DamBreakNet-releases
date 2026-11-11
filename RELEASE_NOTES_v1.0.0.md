# DamBreakNet 1.0.0

The version described in the paper "DamBreakNet: A Hydrograph-Conditioned Convolutional Neural
Network for Dam-Break Flood Mapping". For non-commercial use.

## Files

- `DamBreakNet_v1.0.0.zip`: the QGIS plugin, with the engine, the three trained models and two
  prepared demo dams (Pirapama and Nilo Coelho). Install it with QGIS "Install from ZIP".
- `environment.yml` and `requirements.txt`: only if you manage the engine's Python yourself.

## What it does

- Finds any of the 28,083 SNISB dams by name, town or code, or on the map, or prepares your own
  dam from a drawn crest and its height, volume and material.
- Builds the terrain, land use, soil, flood domain and breach hydrograph.
- Runs DamBreakNet, LNEC/ANA and HAND on the same inputs, with map-quality flags and a triage
  ("rapid map" or "check with a 2D model").
- Sets up its own engine from the panel and signs in to Earth Engine from the panel.

## New in 1.0.0

### Dams outside Brazil

Draw a dam anywhere in the world under **My own dam**. Outside Brazil, the plugin takes the land
cover from ESA WorldCover 2021 and translates it to the MapBiomas classes DamBreakNet was trained
on. It needs no Earth Engine account for these dams. The dam card and the results warn that
DamBreakNet's accuracy outside Brazil is untested, and the triage rule is the same.

Dams in Brazil keep MapBiomas, and their maps are identical to version 0.2.0 (27 of 27). On two
Brazilian test dams, translated WorldCover instead of MapBiomas changed the flooded area by 3% or
less and did not change the triage. A dam in Argentina ran from the panel with no errors.

## Fixed since 0.2.0

### Engine setup on Windows

On Windows, **Set up the engine** stopped with "remove_all: The directory is not empty" while it
unpacked PyTorch. The paths were too long. micromamba 2 stores its package cache in folders named
after the download address, so the longest PyTorch path reached 287 characters, and Windows allows
260.

Version 1.0.0 fixes this:

- it uses micromamba 1.5.12, which keeps a flat cache;
- it builds the engine in `C:\dbn` (or in `.dbn` in your user folder when `C:\dbn` cannot be
  made), with the cache in a short folder;
- it removes a half-built engine before it tries again.

The longest path is now 209 characters. We checked this on macOS by recreating the Windows paths.
It has not been tested on a Windows computer yet.

If you saw this error, install version 1.0.0 and click **Set up the engine** again.

The trained models and the maps they give are unchanged.

## Known limits

- Outside Brazil, the land cover is translated and DamBreakNet's accuracy is untested.
- Checked on macOS with QGIS 3.44; Windows and Linux are not tested yet.
- New dams in Brazil need a Google Earth Engine project for the land use.
- The licences are proposed and still under review by Stanford's Office of Technology Licensing.
