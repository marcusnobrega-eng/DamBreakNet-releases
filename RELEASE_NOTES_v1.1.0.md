# DamBreakNet 1.1.0

Adds a risk report and a PDF summary to the version described in the paper "DamBreakNet: A
Hydrograph-Conditioned Convolutional Neural Network for Dam-Break Flood Mapping". The maps are
unchanged. For non-commercial use.

## Files

- `DamBreakNet_v1.1.0.zip`: the QGIS plugin, with the engine, the three trained models and two
  prepared demo dams (Pirapama and Nilo Coelho). Install it with QGIS "Install from ZIP".
- `environment.yml` and `requirements.txt`: only if you manage the engine's Python yourself.

## New in 1.1.0

### Risk to people

A new step 5 in the panel reports, after every run:

- the people in the flood at 0.05, 0.30 and 1.00 m for each method, and in the self-rescue zone
  (ZAS). People come from WorldPop 2020 constrained estimates, read through Earth Engine for the
  dam's own area only (about 1 MB or less) and saved with the dam;
- the hazard classes H1 to H6 of the Australian flood hazard guideline (AIDR 2017, Guideline
  7-3, Table 2), from DamBreakNet's maximum depth, velocity and depth × velocity, with the people,
  area, schools, health units, emergency services and roads in each class;
- the self-rescue zone, the flooded area within a distance along the valley from the dam (10 km
  by default, set in Settings), with its people, facilities, roads and settlements.

Facilities and roads come from OpenStreetMap. The layers load in a "Risk" group, and the report
is saved as CSV and JSON in the run's `risk` folder. When the public OpenStreetMap servers are
busy, "Retry OpenStreetMap" asks again.

### PDF summary

"Export report (PDF)" writes a five-page summary in English or Portuguese: the hazard-class and
depth maps, the tables, the flooded facilities with coordinates, the method, and suggested
actions keyed to the dam's numbers. Each action names its source: AIDR (2017), the ANA guide for
emergency action plans (2016) or Resolution ANA 121/2022. The report says it is a rapid screening
that does not replace the dam owner's dam-break study and emergency action plan.

### Layers after a run

Only DamBreakNet and the risk layers are drawn. LNEC/ANA and HAND still load, hidden in
collapsed groups, so you can tick them to compare.

## Good to know

- Population needs an Earth Engine project, now also for dams outside Brazil. Without one, the
  report has no people, and the rest still works. The demo dams come with their population and
  OpenStreetMap data.
- The paper used the WorldPop 2025 file for Brazil. WorldPop 2020 gave 3% more people in the
  flood at Pirapama and 62% more at Nilo Coelho, where the count is small and rural.
- The ZAS here is a distance along the valley. Resolution ANA 121/2022 uses the distance the wave
  reaches in 30 minutes, which these maps do not give.
- The hazard classes use the maximum depth and velocity, which may not happen at the same time,
  so they lean high.
- Tested on macOS with QGIS 3.44 on the two demo dams and a dam in Argentina. Windows and Linux
  are not tested yet.
