# DamBreakNet 0.2.0 (test)

First test version for non-commercial users.

## Files

- `DamBreakNet_v0.2.0.zip`: the QGIS plugin, with the engine, the three trained seeds and
  two prepared demo dams (Pirapama and Nilo Coelho). Install it with QGIS "Install from ZIP".
- `environment.yml` and `requirements.txt`: the Python packages the engine needs.

## What it does

- Finds any of the 28,083 SNISB dams by name, town or code, or on the map.
- Prepares a dam outside SNISB from a drawn crest and its height, volume and material.
- Runs DamBreakNet, LNEC/ANA and HAND on the same inputs, with map-quality flags and a
  triage.
- Shows each preparation step and its time, and plain reasons when something fails.

## Known limits

- Dams in Brazil only.
- Checked on macOS with QGIS 3.44; Windows and Linux are not tested yet.
- New dams need a Google Earth Engine project for the land use.
- The licences are proposed and still under review.
