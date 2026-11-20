# Indian Medicinal Crops – Cultivation & Wholesale Price Dataset (2015–2024)

A structured dataset of 13 Indian medicinal crops, combining their growing conditions, yield and cultivation cost with yearly national wholesale market prices from 2015 to 2024.

## Files

| File | Rows | Description |
|---|---|---|
| `crop_conditions.csv` | 13 | One row per crop: names, plant type, climate, soil, light, propagation, time to harvest, yield and cultivation cost |
| `wholesale_price_history_2015_2024.csv` | 61 | Wholesale price of each crop per year, with grade and source link |
| `medicinal_crops_panel_2015_2024.csv` | 61 | One row per crop per year: crop conditions + that year's price, inflation-adjusted cost, revenue, profit and profit class |

### How the files connect

```
crop_conditions (crop_id) ──┐
                            ├── medicinal_crops_panel (crop_id, year) ── wholesale_price_history (crop_id, year)
```

## Crops included

| Scientific name | Common name |
|---|---|
| Alpinia galanga | Kulanjan |
| Asparagus racemosus | Shatavar |
| Bacopa monnieri | Brahmi |
| Curculigo orchioides | Kali musli |
| Hedychium spicatum | Kapoor kachri |
| Hemidesmus indicus | Anantmool |
| Nardostachys grandiflora | Jatamansi |
| Picrorhiza kurroa | Kutki |
| Plumbago zeylanica | Chitrak |
| Swertia chirata | Chirayata |
| Terminalia arjuna | Arjun |
| Terminalia chebula | Harad |
| Tinospora cordifolia | Giloy |

Years covered: 2015, 2016, 2017, 2018, 2021, 2023, 2024.

## Sources

1. **Agro-techniques of Selected Medicinal Plants, Volume I** – National Medicinal Plants Board (NMPB), Department of AYUSH, Government of India (2008).
   A government handbook giving cultivation practices for 50 medicinal plants. For each plant it covers botanical and traditional names, parts used, climate and soil needs, propagation, planting, irrigation, harvesting, yield per hectare, cost of cultivation and market notes.
   Used for: crop conditions, yield and cultivation cost.
   https://www.nmpb.nic.in/sites/default/files/publications/Agro_techniques_of_selected_medicinal_plants_Vol-I.pdf

2. **Van Dhan Vyapar – National wholesale market rates of medicinal plants** – State Forest Research Institute, Jabalpur, Government of Madhya Pradesh (quarterly newsletter).
   Used for: yearly wholesale prices (Rs/kg). The last month of each issue was taken. Links for each issue are in `wholesale_price_history_2015_2024.csv`.

3. **Consumer Price Index for Agricultural Labourers (CPI-AL)** – Labour Bureau, Government of India, via RBI Handbook of Statistics on the Indian Economy, Table 37.
   Used for: adjusting the cultivation cost to each year's price level.
   https://website.rbi.org.in/documents/d/rbi/37t_hbs-2024-25_29082025

## Column guide

### crop_conditions.csv
| Column | Meaning |
|---|---|
| `crop_id` | Unique crop ID (NMPB_V1_xxx) |
| `scientific_name`, `common_name`, `family` | Plant identity |
| `ayurvedic_name`, `unani_name` | Traditional medicine names |
| `parts_used` | Parts used in medicine |
| `traded_part` | Part sold in the market |
| `habit` | Herb / Shrub / Climber / Tree |
| `life_cycle` | Annual / Perennial |
| `crop_category` | Crop duration group |
| `climate_zone` | Tropical / Subtropical / Temperate / Alpine |
| `soil_type`, `light` | Preferred soil and light |
| `propagation` | Seed / Vegetative / Both |
| `harvest_months` | Months from planting to harvest |
| `harvest_pattern`, `harvests_per_year` | One-time or recurring harvest |
| `yield_kg_ha`, `yield_basis` | Yield in kg per hectare (dry weight) |
| `cost_rs_ha_2006_07`, `cost_period_years` | Cost of cultivation (Rs/ha) and the period it covers |
| `printed_pages` | Pages in the NMPB book |

### wholesale_price_history_2015_2024.csv
| Column | Meaning |
|---|---|
| `crop_id`, `scientific_name`, `year` | Keys |
| `period` | Month of the price |
| `price_low`, `price_high`, `price_mid` | Wholesale price range and midpoint (Rs/kg) |
| `grade_as_printed` | Grade/name as printed in the newsletter |
| `source`, `url` | Source of the price |

### medicinal_crops_panel_2015_2024.csv
Contains the crop conditions above, plus:
| Column | Meaning |
|---|---|
| `year`, `price_period` | Year and month of the price |
| `cpi_fy`, `cpi_al` | Financial year and CPI-AL value used |
| `cost_rs_ha` | Cultivation cost adjusted to that year (Rs/ha) |
| `price_rs_kg` | Wholesale price that year (Rs/kg) |
| `price_change_pct_vs_prev` | % change from the previous available year |
| `gross_revenue_rs_ha` | Yield − cost |
| `net_profit_rs_ha` | Revenue − cost |
| `roi_pct` | Return on investment (%) |
| `net_profit_per_year_rs_ha` | Net profit spread over the crop duration |
| `profit_label` | Low (< ₹1 lakh), Medium (₹1–4 lakh), High (> ₹4 lakh) net profit per hectare per year |

## How values were calculated

- Ranges (e.g. "Rs 250–300") were converted to their midpoint.
- Yield units (quintals, tonnes) were converted to kg per hectare.
- Adjusted cost = book cost × (CPI-AL of that year ÷ CPI-AL of 2006-07).
- Recurring crops use annual revenue and annualised cost; one-time crops spread profit over the months to harvest.

## License & use

The data is compiled from publicly available Government of India and Government of Madhya Pradesh publications. Please cite the original sources listed above when using this dataset.
