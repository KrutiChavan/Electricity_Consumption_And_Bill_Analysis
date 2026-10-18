# Electricity Consumption and Bill Analysis

A Python desktop application that analyzes monthly electricity consumption and bills. Enter the month, units consumed (kWh) and bill amount, or load them from a CSV file, and the app cleans the data, calculates summary statistics, detects unusual increases in consumption, and shows everything as tables, alerts and graphs in a Tkinter GUI.

Built with **Python, Pandas, NumPy, Matplotlib and Tkinter**. No API or Machine Learning is required.

---

## Features

- **Easy data entry:** add records through a form (month, units, bill), or load a CSV file. Sample data is built in for a quick demo.
- **Data cleaning and validation (Pandas):** fixes column names, converts data types, removes missing or invalid rows, replaces duplicate months and sorts by month.
- **Consumption and bill analysis:** total units, total bill, average units per month, average bill per month, average cost per unit, and the months with the highest and lowest bills.
- **Month-to-month comparison:** percentage change in both units and bill for every month.
- **Unusual increase detection:** a month is flagged when its units rise by at least a chosen percentage (default 20%) compared with the previous month. The threshold can be changed in the GUI and results update instantly.
- **Trend and estimate (NumPy):** finds whether consumption is increasing or decreasing, estimates the next month's units and bill, and shows the correlation between units and bill.
- **Graphs (Matplotlib):** monthly consumption bar chart with a trend line and a monthly bill line graph. Unusual months are shown in red.
- **Export:** save the analyzed report as a CSV file.

## Screenshots

| Data Entry | Monthly Table (sample data) |
|---|---|
| ![Data Entry](screenshots/01-data-entry.png) | ![Monthly Table](screenshots/02-monthly-table.png) |

| Analysis & Alerts | Graphs |
|---|---|
| ![Analysis and Alerts](screenshots/03-analysis-alerts.png) | ![Graphs](screenshots/04-graphs.png) |

## How It Works

```
Enter Data -> Process Data (Pandas) -> Analyze Consumption & Bill -> Detect Unusual Increase -> Generate Graphs (Matplotlib) -> Display in Tkinter GUI
```

| Step | Function / Method | Library |
|---|---|---|
| Enter data | `App._add_row()`, `App._load_csv()` | Tkinter, Pandas |
| Process data | `process_data()` | Pandas |
| Analyze consumption and bill | `analyze()` | Pandas, NumPy |
| Detect unusual increase | `detect_unusual()` | Pandas |
| Generate graphs | `App._update_graphs()` | Matplotlib, NumPy |
| Display results | `App._update_table()`, `App._update_summary()` | Tkinter |

Every change (adding, deleting or loading data, or changing the threshold) runs the whole pipeline again through the `refresh()` method, so the table, alerts and graphs are always up to date.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Pandas | Data cleaning, processing, totals, averages and percentage changes |
| NumPy | Trend line, next-month estimate and correlation |
| Matplotlib | Consumption and bill graphs embedded in the GUI |
| Tkinter | Graphical user interface |

## Getting Started

### Prerequisites

- Python 3.9 or later
- Tkinter (included with the standard Python installer on Windows and macOS; on Ubuntu/Debian install it with `sudo apt install python3-tk`)

### Installation

```bash
git clone https://github.com/KrutiChavan/Electricity_Consumption_And_Bill_Analysis.git
cd Electricity_Consumption_And_Bill_Analysis
pip install -r requirements.txt
```

### Run

```bash
python electricity_bill_analysis.py
```

## Usage

1. Click **Load Sample Data** to try the app instantly, or enter your own data:
   - type the **Month** (`YYYY-MM`), **Units (kWh)** and **Bill amount**, then click **Add / Update**
   - or click **Load CSV** to import a file
2. Open the **Data Entry** tab to see the table. Months with an unusual increase are highlighted in red.
3. Change the **threshold (%)** to make the detection more or less sensitive.
4. Open the **Analysis & Alerts** tab for the summary, alerts, trend and next-month estimate.
5. Open the **Graphs** tab to see the consumption and bill graphs.
6. Click **Save CSV** to export the analyzed report.

### CSV format

The file must have a header row with these three columns:

```csv
month,units,bill
2025-01,210,1320
2025-02,198,1262
2025-03,225,1443
```

A ready-to-use example is included as [`sample_data.csv`](sample_data.csv).

Rows with missing or invalid values, zero or negative units, or negative bills are removed. If the same month appears more than once, the last entry is kept.

### How unusual increases are detected

```
units change % = (units this month - units last month) / units last month x 100
```

A month is marked **UNUSUAL INCREASE** when its units change % is greater than or equal to the threshold (default 20%). The first month is never flagged because it has no previous month to compare with.

## Project Structure

```
.
├── electricity_bill_analysis.py   # main application (logic + GUI)
├── sample_data.csv                # example input file
├── requirements.txt               # Python dependencies
├── screenshots/                   # images used in this README
└── README.md
```

## Limitations

- The bill is entered by the user; it is not calculated from tariff slabs.
- The next-month estimate uses a simple straight-line trend, so it is only a rough guide.
- Data is not stored between runs unless it is saved to a CSV file.

## Future Scope

- Calculate the bill automatically from tariff slabs, fixed charges and taxes
- Store data in a database such as SQLite
- Give simple energy-saving suggestions based on high-consumption months
- Support multiple meters, rooms or appliances
- Export reports as PDF or Excel and improve prediction using seasonal data

## Author

**Kruti Chavan**
GitHub: KrutiChavan(https://github.com/KrutiChavan)
