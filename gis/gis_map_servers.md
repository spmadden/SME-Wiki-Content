---
title: gis_map_servers
description: 
published: 1
date: 2025-11-27T16:02:21.893Z
tags: 
editor: markdown
dateCreated: 2023-09-11T01:28:20.693Z
---

## XYZ Tile Servers

### Free

-   [US National Map Data](https://apps.nationalmap.gov/viewer/)
    -   [USGS Imagery Only](https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fbasemap.nationalmap.gov%2Farcgis%2Frest%2Fservices%2FUSGSImageryOnly%2FMapServer&source=sd)
        -   `https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer/tile/{z}/{y}/{x}`
    -   [USGS Imagery+Topo](https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fbasemap.nationalmap.gov%2Farcgis%2Frest%2Fservices%2FUSGSImageryTopo%2FMapServer&source=sd)
        -   `https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryTopo/MapServer/tile/{z}/{y}/{x}`
    -   [USGS Imagery+Hydro](https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fbasemap.nationalmap.gov%2Farcgis%2Frest%2Fservices%2FUSGSHydroCached%2FMapServer&source=sd)
        -   `https://basemap.nationalmap.gov/arcgis/rest/services/USGSHydroCached/MapServer/tile/{z}/{y}/{x}`
    -   [USGS Shaded Relief Terrain](https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fbasemap.nationalmap.gov%2Farcgis%2Frest%2Fservices%2FUSGSShadedReliefOnly%2FMapServer&source=sd)
        -   `https://basemap.nationalmap.gov/arcgis/rest/services/USGSShadedReliefOnly/MapServer/tile/{z}/{y}/{x}`
    -   [USGS Blank Basemap](https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fbasemap.nationalmap.gov%2Farcgis%2Frest%2Fservices%2FUSGSTNMBlank%2FMapServer&source=sd)
        -   `https://basemap.nationalmap.gov/arcgis/rest/services/USGSTNMBlank/MapServer/tile/{z}/{y}/{x}`
    -   [USGS Topo](https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fbasemap.nationalmap.gov%2Farcgis%2Frest%2Fservices%2FUSGSTopo%2FMapServer&source=sd)
        -   `https://basemap.nationalmap.gov/arcgis/rest/services/USGSTopo/MapServer/tile/{z}/{y}/{x}`
-   The OpenStreetMap family of data
    -   [OpenStreetMap](https://www.openstreetmap.org/)
        -   `https://tile.openstreetmap.org/{z}/{x}/{y}.png`
    -   [OpenTopoMap](https://opentopomap.org/)
        -   `https://tile.opentopomap.org/{z}/{x}/{y}.png`
        -   [GitHub](https://github.com/der-stefan/OpenTopoMap)
    -   [OpenStreetMap's List](https://apps.fs.usda.gov/arcx/rest/services/EDW/EDW_FSTopo_01/MapServer/tile/{z}/{y}/{x}) - many NON FREE.
-   [USFS FSTopo](https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fapps.fs.usda.gov%2Farcx%2Frest%2Fservices%2FEDW%2FEDW_FSTopo_01%2FMapServer&source=sd)
    -   `https://apps.fs.usda.gov/arcx/rest/services/EDW/EDW_FSTopo_01/MapServer/tile/{z}/{y}/{x}`

### Non-Free

-   [CalTopo](https://caltopo.com/map.html)
    -   `https://img.caltopo.com/tile/mbt/{z}/{x}/{y}.png`
-   [ArcGIS Basemaps](https://arcg.is/11iLrH)

## Raster Datasets

-   [FAA Sectionals](https://www.faa.gov/air_traffic/flight_info/aeronav/digital_products/vfr/)
    -   GeoTIFF, GeoPDF, no processing needed
-   LANDSAT Data
    -   Raw pixel data in GeoTIFF, needs processing to turn into pretty pictures
    -   [USGS EarthExplorer](https://earthexplorer.usgs.gov/) - needs free account
    -   [AWS S3](https://registry.opendata.aws/usgs-landsat/) - requires payment
-   USGS Topo Maps
    -   [AWS S3](https://prd-tnm.s3.amazonaws.com/index.html?prefix=StagedProducts/Maps/USTopo/PDF/) - no payment needed
-   USFS Topo Maps
    -   <https://data.fs.usda.gov/geodata/rastergateway/states-regions/states.php>
    - <https://apps.fs.usda.gov/arcx/rest/services>
-   DTED/DEM Terrain Data
    -   [USGS EarthExplorer](https://earthexplorer.usgs.gov/)
        -   DTED0, DTED1, DTED2
    -   [NationalMap DEMs](https://www.usgs.gov/3d-elevation-program/about-3dep-products-services)
        -   Up to 1m terrain resolution (chonky set)
-   [NASA Blue Marble](https://visibleearth.nasa.gov/collection/1484/blue-marble)
    -   JPEG in equidistant rectangular
- FEMA GIS
  - <https://services2.arcgis.com/FiaPA4ga0iQKduv3/ArcGIS/rest/services>
  
- Fire Fly GIS World Imagery
  - <https://fly.maptiles.arcgis.com/arcgis/rest/services/World_Imagery_Firefly/MapServer>
  
- FL Keys Reef Maps
  - <https://ocean.floridamarine.org/arcgis/rest/services/Projects_FWC/Unified_Florida_Reef_Tract_Map_FWC/MapServer>
  
## Vector Datasets

-   [US Forest Service](https://data.fs.usda.gov/geodata/edw/datasets.php?xmlKeyword=FSTopo)
    -   Shapefiles
-   [NOAA ENCs](https://charts.noaa.gov/ENCs/ENCs.shtml)
-   [NaturalEarth Data](https://www.naturalearthdata.com/downloads/)
    -   Shapefiles, GeoPKGs
-   [OpenStreetMap](https://planet.openstreetmap.org/)
    -   Raw PBFs in the OSM format
-   [National Parks Service](https://mapservices.nps.gov/arcgis/rest/services/NationalDatasets)
    -   ArcGIS REST servers, roads, trails, maps, POIs
-   [Massachusetts GIS Data Layers](https://www.mass.gov/info-details/massgis-data-layers)
	- https://massgis.maps.arcgis.com/home/user.html?user=MassGIS
  - MA GIS WMS: https://gis-prod.digital.mass.gov/geoserver/wms
- USGS Quakes
  - <https://earthquake.usgs.gov/arcgis/rest/services>
- VA Energy GIS
  - <https://www.energy.virginia.gov/gis/rest/services/>

## OpenStreetMap Links

-   [Zoom Levels](https://wiki.openstreetmap.org/wiki/Zoom_levels)
-   [Protobuf Data Dump Format](https://wiki.openstreetmap.org/wiki/PBF_Format)
-   [Data Dumps](https://wiki.openstreetmap.org/wiki/Planet.osm)
-   Styles
    -   [Default Style](https://github.com/gravitystorm/openstreetmap-carto)
