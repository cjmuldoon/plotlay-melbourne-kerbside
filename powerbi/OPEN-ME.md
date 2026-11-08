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
3. Check the numbers (below).

If the report was updated while open, close Power BI and reopen the .pbip rather than using Apply external changes. (After Apply external changes one export drew the page at about 57% inside a much larger canvas; a full close and reopen put it right.)

## Check the numbers after Refresh

After **Refresh**, on **The kerb through a day**:

| Card | Should read |
|---|---|
| Bays occupied, weekdays 8 am to 8 pm | 56.3% |
| Average stay, minutes | 58.8 |
| Cars a bay a day | 10.8 |

The weekday line peaks at 66.5% at 11 am, dips to 46.0% at 5 pm and rises to 61.6% at 7 pm; the weekend line peaks at 65.5% at 1 pm.

On **Streets by hour** the slicers open on **11** and **Weekday** (one value each); the map then shades each street by how full it was at 11 am on weekdays (the streets average 66.5%). If both slicers are cleared the map still shows 11 am on weekdays. On **How long** (streets with 10 bays or more) the stay chart starts with Airlie St, Clowes St to The Righi (217 minutes) and the cars chart with Collins St, Queen St to Elizabeth St (44.9).

## The model

- **Kerb**: one row per street (`data/kerb/kerb_segments.csv`), keyed by `seg_id`, with bays, stays and the 2019 summaries.
- **Hours**: `kerb_hours.csv`, one row per street, day type and hour, with the share of bays occupied.
- **HourOfDay** and **DayType**: for the slicers. `Share occupied` always uses one hour of one day type: the ones picked, or 11 am on a weekday when none is.

## The map

- **Shape Map** (Streets by hour page). The custom map, `data/geometry/kerb.topojson`, is saved inside the report (`MelbourneKerbside.Report/StaticResources/RegisteredResources/kerb.topojson`, a copy that keeps only the street code), so the streets draw on open, shaded by how full they were in the hour and day picked. The Shape Map has no base map of its own, so the file also carries the context: the suburbs (ABS, CC BY 4.0) in a pale ground tone, the City of Melbourne boundary as a thin line, and the Yarra, Moonee Ponds Creek and Victoria Harbour showing as the map's pale blue background (their outline from Vicmap Hydro, CC BY 4.0). Loading the plain file from `data/` by hand (below) gives the streets without that context. If the map shows the United States instead (an older Desktop can ignore a saved map): select it, then **Format visual** (the paintbrush), **Visual**, **Map settings**, **Map type: Custom map**, **Add map type** (or **Browse**), and choose `..\data\geometry\kerb.topojson`. Under **View map keys** the street codes (20001, 21860...) should be matched. If the Shape Map is not in the Visualizations pane at all, turn it on in **File, Options and settings, Options, Preview features, Shape map visual** and restart Desktop.

If the map comes up empty, drag the fields back: Location `Kerb[seg_id]`, Color saturation `[Share occupied]`.

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
