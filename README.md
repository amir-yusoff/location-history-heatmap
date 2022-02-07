# Location History Heatmap

This is a script that generates an interactive geo heatmap from your Google location history data using Python, Folium and OpenStreetMap.

- [Location History Heatmap](#location-history-heatmap)
  - [1. Get Your Location Data](#1-get-your-location-data)
  - [2. Clone This Repository](#2-clone-this-repository)
  - [3. Install Dependencies](#3-install-dependencies)
  - [4. Run the Script](#4-run-the-script)
  - [5. Review the Results](#5-review-the-results)


## 1. Get Your Location Data

Here you can download all of the data that Google has [stored on you](https://takeout.google.com/)

To use this script, you only need to select and download your "Location History", which Google will provide to you as a JSON file by default.  KML is also an output option and is accepted for this program.


## 2. Clone This Repository

Click the green "Clone or Download" button at the top right of the page. If you want to get started with this script more quickly, click the "Download ZIP" button, and extract the ZIP somewhere on your computer.

## 3. Install Dependencies

In a promp or Terminal window, type:

```shell
pip install -r requirements.txt
```
or if you're using Anaconda:
```shell
conda install --file requirements.txt 
```

There might be a problem installing folium, I've found that a workaround on this is to run this:
```shell
conda install -c conda-forge folium
```

## 4. Run the Script

In the same command prompt or Terminal window, type the following, and press enter:

```shell
python geo_heatmap.py <file> [<file> ...]
```

Replace the string `<file>` from above with the path to any of the following files:

- The `Location History.json` JSON file from Google Takeout
- The `Location History.kml` KML file from Google Takeout
- The `takeout-*.zip` raw download from Google Takeout that contains either of the above files
- A [GPS Exchange Format (GPX)](https://en.wikipedia.org/wiki/GPS_Exchange_Format) file


<details>
  <summary>Examples</summary>
 
Single file:

```shell
python geo_heatmap.py C:\Users\Testuser\Desktop\locations.json
```

```shell
python geo_heatmap.py "C:\Users\Testuser\Desktop\Location History.json"
```

```shell
python geo_heatmap.py locations.json
```

Multiple files:

```shell
python geo_heatmap.py locations.json locations.kml takeout.zip
```

Using the stream option (for users with Memory Errors):

```shell
python geo_heatmap.py -s locations.json
```

Set a date range:

```shell
python geo_heatmap.py --min-date 2017-01-02 --max-date 2018-12-30 locations.json
```

Advanced heatmap settings:

```shell
python geo_heatmap.py -z 15 -r 12 -b 7 -mo 0.3 -mz 20 locations.json
```
</details>

<details>
  <summary>Usage</summary>

```
usage: geo_heatmap.py [-h] [-o OUTPUT] [--min-date YYYY-MM-DD]
                      [--max-date YYYY-MM-DD] [-s] [--map MAP] [-z ZOOM_START]
                      [-r RADIUS] [-b BLUR] [-mo MIN_OPACITY] [-mz MAX_ZOOM]
                      file [file ...]

positional arguments:
  file                  Any of the following files:
                        - Your location history JSON file from Google Takeout
                        - Your location history KML file from Google Takeout
                        - The takeout-*.zip raw download from Google Takeout
                        that contains either of the above files
                        - A GPX file containing GPS tracks

optional arguments:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        Path of heatmap HTML output file.
  --min-date YYYY-MM-DD
                        The earliest date from which you want to see data in the heatmap.
  --max-date YYYY-MM-DD
                        The latest date from which you want to see data in the heatmap.
  -s, --stream          Option to iteratively load data.
  --map MAP, -m MAP     The name of the map tiles you want to use.
                        (e.g. 'OpenStreetMap', 'StamenTerrain', 'StamenToner', 'StamenWatercolor')
  -z ZOOM_START, --zoom-start ZOOM_START
                        The initial zoom level for the map. (default: 6)
  -r RADIUS, --radius RADIUS
                        The radius of each location point. (default: 7)
  -b BLUR, --blur BLUR  The amount of blur. (default: 4)
  -mo MIN_OPACITY, --min-opacity MIN_OPACITY
                        The minimum opacity of the heatmap. (default: 0.2)
  -mz MAX_ZOOM, --max-zoom MAX_ZOOM
                        The maximum zoom of the heatmap. (default: 4)
```
</details>

## 5. Review the Results

The script will generate a HTML file named `heatmap.html`. This file will automatically open in your browser once the script completes. Enjoy!
