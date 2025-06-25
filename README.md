# Tile Manager

## Overview
This Python script processes map tiles within the MDC urban boundary using the HowLoud API. It supports three main modes:
- **Dry Run**: Lists the tile URLs and file paths without creating files or making API requests.
- **Generate Mode**: Creates a directory structure with placeholder `.png` files to outline the required tiles.
- **Download Mode**: Downloads real map tiles from the HowLoud API, saving them to the appropriate directories.

The tiles are processed across a configurable zoom level range and are spatially filtered to only include tiles that intersect the provided urban boundary.

---

## Prerequisites
- Python 3.x
- Python packages:
  - `requests`
  - `geopandas`
  - `shapely`
- A HowLoud API key stored in a file named `key.txt`.
- An urban boundary GeoJSON file at `data/urban_boundary.geojson`.

---

## Usage

```bash
python script.py [MODE] [OPTIONS]
```

### Modes
- `-g` or `--generate`:  
  Create the directory structure and placeholder files for all relevant tiles.

- `--request`:  
  Download real tiles from the API and save them locally.

*(Note: You must choose either `--generate` or `--request`, or neither for a dry run.)*

---

## Options
| Flag               | Description                                               | Default |
|--------------------|-----------------------------------------------------------|---------|
| `--overwrite`      | Overwrite existing files when downloading tiles.           | False   |
| `--max-downloads N`| Maximum number of tiles to download (applies to `--request`).| 5       |
| `--zoom-min N`     | Minimum zoom level to process.                             | 8       |
| `--zoom-max N`     | Maximum zoom level to process.                             | 14      |

---

## Examples

### 1. Dry Run (Preview tile URLs and paths)
```bash
python script.py
```

### 2. Generate directory structure with placeholder files
```bash
python script.py --generate --zoom-min 10 --zoom-max 12
```

### 3. Download up to 10 tiles (skip existing files)
```bash
python script.py --request --max-downloads 10
```

### 4. Force download and overwrite all existing tiles
```bash
python script.py --request --overwrite --max-downloads 50
```

---

## File Structure Example
When generating or downloading, tiles are saved in the following structure:
```
tiles/
└── {zoom}/
    └── {x}/
        └── {y}.png
```
Example:
```
tiles/12/654/1582.png
```

---

## Notes
- The API key must be saved in a file named `key.txt` in the same directory as the script.
- The urban boundary GeoJSON should be located at `data/urban_boundary.geojson`.
