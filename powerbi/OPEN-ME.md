# Opening the Power BI report

`MelbourneKerbside.pbip` is a Power BI Project: the report (`MelbourneKerbside.Report`, PBIR format) and the semantic model (`MelbourneKerbside.SemanticModel`, TMDL) saved as text, so the repo can show every change. Power BI Desktop opens it like a `.pbix`.

## What you need

- Power BI Desktop for Windows, a recent version (2026). If Desktop is older than about mid 2025, turn on **File, Options and settings, Options, Preview features, Power BI Project (.pbip) save option** and **Store reports using enhanced metadata format (PBIR)**, then restart Desktop.
- The repo folder on the Windows machine. In Parallels the Mac home folder is usually shared as `\\Mac\Home`.

## Open it

1. In Windows, go to the repo's `powerbi` folder and double-click `MelbourneKerbside.pbip`.
2. The visuals are empty the first time. Select **Refresh** on the Home ribbon.
   - By default the data is read from the repo's public copy on GitHub (`DataFolder` is `https://raw.githubusercontent.com/cjmuldoon/plotlay-melbourne-kerbside/main/data/`). If Desktop asks how to connect, choose **Anonymous** and then **Connect**.
   - To read the files from disk instead, go to **Home, Transform data, Edit parameters** and set `DataFolder` to the full path of the repo's `data` folder, **ending with a backslash**. Then select **OK** and **Apply changes**.
   - If Desktop warns about privacy levels, choose **Ignore privacy levels** (all the sources are public open data).
3. After the refresh, check page 1: the weekday line peaks at about the README's weekday figure in the late morning and dips at 5 pm.

## The model

- **Kerb**: one row per street (`data/kerb/kerb_segments.csv`), keyed by `seg_id`, with bays, stays and the 2019 summaries.
- **Hours**: `kerb_hours.csv`, one row per street, day type and hour, with the share of bays occupied.
- **HourOfDay** and **DayType**: for the slicers.

## Two map settings Power BI asks for by hand

- **Shape Map** (page 1). Select the map. In **Format visual, Visual, Map settings**, set the map type to **Custom map**, choose **Add map type**, and pick `..\data\geometry\kerb.topojson`. Under **View map keys** the seg_id values should match. If the Shape Map isn't in the Visualizations pane, turn it on in **Options, Preview features, Shape map visual**.
If a map visual comes up empty, drag the fields back:
- Shape Map: Location `Kerb[seg_id]`, Color saturation `[Occupied]`.

Then save with **File, Save**, and if you like **File, Save as** a `.pbix`, which includes the data.

## Publish (only if you choose to)

Use **Home, Publish**. In the Power BI service, set the semantic model's **Data source credentials** for the GitHub address to **Anonymous**. Scheduled refresh then works with no gateway. **Publish to web** makes a public link, so only use it if you mean the report to be public.

## Shot list for the website and the video

| # | Shot | How | Length |
|---|---|---|---|
| 1 | The kerb through a day | page 1 | still |
| 2 | Streets at 11 am and 5 pm, weekday | the slicers | 2 stills |
| 3 | How long | page 3 | still |

Keep the footer with the attribution visible in every shot.
