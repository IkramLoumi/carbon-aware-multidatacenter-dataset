# carbon-aware-multidatacenter-dataset
# A Real-World, Multi-Datacenter Dataset for Carbon-Aware Cloud Task Scheduling

Authors: BOUMEDJOUT Amal, LOUMI Ikram — École Nationale Polytechnique d'Oran – Maurice Audin, Algeria

This repository contains the derived infrastructure dataset (72 data-center sites, 17 countries)


## Repository structure

carbon-aware-multidatacenter-dataset/
├── README.md
├── LICENSE
├── requirements.txt
├── data/
│   └── datacenters_72.csv        


## What is NOT included

The **Google Cluster Trace (May 2019, ~50 GB)** is not redistributed here. Please obtain it from its official source: [https://github.com/google/cluster-data?utm_source=chatgpt.com] and follow its own terms of use.

## Dataset description

One row per data-center site (72 rows, no missing values in the required columns).

| Column | Description | Unit | Source | Data year |
| --- | --- | --- | --- | --- |
| `capacity_mw` | Installed capacity | MW | Operator / Equinix API / Digital Realty / DataCenterMap / Baxtel / Uptime Institute 2023 (see `capacity_mw_source`) | 2022–2024 |
| `capacity_mw_source` | Provenance tier of `capacity_mw` (direct value vs. estimate such as `operator_kb_uptime_2023`, `country_avg_uptime_2023`) | – | – | – |
| `pue` | Power Usage Effectiveness (campus-level for Google, fleet average for other operators) | ratio | Operator sustainability reports | 2022–2023 |
| `carbon_intensity` | National grid carbon intensity | gCO₂/kWh | Our World in Data / Ember / IEA | 2022 |
| `renewable_pct` | National renewable electricity share | % | Our World in Data / Ember / IEA | 2022 |
| `electricity_cost` | National industrial electricity tariff | USD/kWh | IEA World Energy Prices | 2023 |
| `latitude`, `longitude` | Site coordinates | degrees | OpenStreetMap / Overpass | – |
<!-- TODO: add the remaining columns of the Excel file (name, operator, country, city, ...) -->

## Method (summary)

- 8,691 candidate locations collected (OpenStreetMap/Overpass, Baxtel, PeeringDB, DataCenterMap) → 4,703 after deduplication → 72 sites retained after requiring all core attributes.
- No value was imputed or interpolated. Sites lacking a required value were excluded.
- Country assignment: Overpass `addr:country`, otherwise Nominatim reverse geocoding (zoom 6). Ambiguous sites were excluded.

## Limitations

- Carbon intensity and renewable share are **national** indicators; they do not capture subnational grid variation, PPAs or on-site generation.
- PUE for most operators is a fleet average, not a site measurement.
- The data combine different reference years (workload 2019; infrastructure 2022–2024); no temporal interpolation is applied. The dataset is a static, mixed-period benchmark, not an operational snapshot.


