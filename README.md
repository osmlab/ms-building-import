# ms-building-import
This repository showcases the [Microsoft 9.8 million](https://wiki.openstreetmap.org/wiki/Microsoft_Building_Footprint_Data
) US buildings in Mapbox GL JS which is licensed under [ODbL](https://wiki.openstreetmap.org/wiki/Open_Database_License). The dataset contains both building shapes and height information of all major cities in 45 US states. To visualise in Mapbox Studio, we have to convert from `shape` -> `geojson` -> `mbtiles` files.

### Data extraction and conversion
- All the state data are in [shape file format](https://wiki.openstreetmap.org/wiki/Microsoft_Building_Footprint_Data#Data_Catalog). This data needs conversion and cleanup to visualise better. There are the 3 steps to follow.

#### Step 1: Convert shape file to GeoJSON
- Download [ogr2ogr](https://trac.osgeo.org/gdal/wiki/DownloadingGdalBinaries) and install it based on the Operating system you are using.
- Download the building dataset, unzip the contents, and enter into the state folder in your terminal.
- Use `ogr2ogr` to convert the shape files to GeoJSON.

   `ogr2ogr -f GeoJSON -t_srs crs:84 state_name.geojson *.shp`

   ```
   E.g. For Florida state,

   ogr2ogr -f GeoJSON -t_srs crs:84 state_name.geojson *.shp

   ```
#### Step 2: Generate mbtiles from GeoJSON using tippecanoe
- Generate mbtiles using [tippecanoe](https://github.com/mapbox/tippecanoe),

   `tippecanoe -fo state_name.mbtiles -l custom -z12 -Z12 state_name.geojson`

 - If you want to append all states GeoJSON to a single `mbtiles`, use `-F` option of tippecanoe. Make sure you've given common output mbtiles and change the input GeoJSON file.

   `tippecanoe -Fo microsoft-buildings.mbtiles -l custom -z12 -Z12 state_name.geojson`


#### Step 3: Upload mbtiles to Mapbox Studio
- Create [Mapbox Studio](https://www.mapbox.com/signup/) account
- Upload mbtiles in `Tilesets` section.
