# HDF5 with Pandas Project

This project demonstrates how to work with **HDF5 files** using Python and the `pandas` library.  
The goal is to store multiple CSV datasets (e.g., yearly AQI data) into a single HDF5 file for efficient storage and retrieval.

---

## Requirements

Make sure you have the following libraries installed:

```bash
sudo apt install python3-pandas python3-tables python3-h5py
```

or (latest versions via pip):

```bash
python3 -m pip install pandas tables h5py --break-system-packages
```

---

## Project Structure

```
├── aqi_2022.csv
├── aqi_2023.csv
├── aqi_2024.csv
├── aqi_2025.csv
├── aqi.h5
├── script.py
└── README.md
```

---

## Usage

### 1. Save CSV files into an HDF5 file
```python
import pandas as pd

with pd.HDFStore('aqi.h5', mode='w') as store:
    for year in range(2022, 2026):
        df = pd.read_csv(f'aqi_{year}.csv')
        store.put(f"year_{year}", df)
```

### 2. Read data back from HDF5
```python
with pd.HDFStore('aqi.h5', mode='r') as store:
    print(store.keys())  # list of datasets inside HDF5
    df2022 = store['year_2022']
    print(df2022.head())
```

---

## Notes
- Dataset keys in HDF5 should not start with numbers.  
  Use names like `"year_2022"` instead of `"2022"`.
- `HDFStore` is great for structured storage but for big data consider also **Parquet** format (`pandas.to_parquet`).

---

## Author
👤 Behruz Maxmudov  
