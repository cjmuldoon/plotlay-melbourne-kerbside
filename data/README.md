# Data

All files are CC BY 4.0 (see `../LICENSE-DATA` and `../NOTICE`). Coordinates are WGS 84 longitude and latitude.

## geometry/

The council's road corridor outlines that held a 2019 parking sensor, exported from Plotlay. `key` is the corridor's
`seg_id`. With the formula columns worked out in Plotlay: `full_hours_wd` and `full_hours_we` (hours of the day at
85% or fuller), `weekend_vs_weekday`. GeoJSON for Azure Maps, QGIS and Python; TopoJSON for the Power BI Shape Map;
CSV with WKT and centres.

## kerb/

- `kerb_segments.csv`: one row per street (`seg_id`): its name, area, most common sign, `bays`, `stays`, `occ_wd_8_20`
  and `occ_we_8_20` (% of bays occupied 8 am to 8 pm), `avg_stay_min`, `stays_per_bay_day`, `overstay_pct`.
- `kerb_hours.csv`: the share of bays occupied (%) at each hour, `day_type` Weekday or Weekend. `weekday_hours.csv` and
  `weekend_hours.csv`: the same, one table each, as linked in Plotlay.
- `kerb_segments_2019_all.csv`: every kerb segment in the 2019 file (street and cross streets), matched to an outline
  or not, with `short_events_pct` (car-present events under 2 minutes).

How full: each sensor's state read at half past every hour of 2019; a moment no event covers counts for nothing. A stay
is a car-present event of 2 minutes to 24 hours.
