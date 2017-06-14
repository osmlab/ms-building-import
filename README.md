# ms-building-import

This repository showcases the [Microsoft's 9.8 million](https://wiki.openstreetmap.org/wiki/Microsoft_Building_Footprint_Data
) US buildings in Mapbox GL JS which is licensed under [ODbL](https://wiki.openstreetmap.org/wiki/Open_Database_License). 

The dataset contains both building geometry and height information major cities in 44 US states. To visualise in Mapbox Studio, we converted the 
`Shapefiles -> GeoJSON -> MBTiles`.

### Data extraction and conversion
All the state data were in [shapefile format](https://wiki.openstreetmap.org/wiki/Microsoft_Building_Footprint_Data#Data_Catalog). This data needs conversion and cleanup to visualise better.  There are the 3 steps to follow.

#### Step 1. Convert shape file to GeoJSON
- Install `[ogr2ogr](https://trac.osgeo.org/gdal/wiki/DownloadingGdalBinaries)`.
- Download and extract the compressed file. 
- Use `ogr2ogr` to convert the shapefile to GeoJSON.

 `ogr2ogr -f GeoJSON -t_srs EPSG:4326 output.geojson input.shp`

#### Step 2: Generate mbtiles from GeoJSON using tippecanoe
- Generate MBTiles using [Tippecanoe](https://github.com/mapbox/tippecanoe),

 `tippecanoe -fo outout.mbtiles -l custom -z12 -Z12 state_name.geojson`

 - If you want to append all states GeoJSON to a single MBTiles use the `-F` option of Tippecanoe. 
 Make sure you've given common output mbtiles and change the input GeoJSON file.

 `tippecanoe -Fo output.mbtiles -l custom -z12 -Z12 state_name.geojson`

#### Step 3: Upload MBTiles to Mapbox Studio
- Create [Mapbox Studio](https://www.mapbox.com/signup/) account
- Upload the MBTiles in `Tilesets` section and visualise them.
