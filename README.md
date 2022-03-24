# kennedy osm data
extraction of the keyword "ennedy" form the osm data of Italy

a simple bash script based on ``wget``, ``osmium``, ``ogr2ogr``

![](https://raw.githubusercontent.com/napo/kennedy_osm_data/main/img/kennedy_in_italy.png)


```bash
wget https://download.geofabrik.de/europe/italy/centro-latest.osm.pbf
osmium tags-filter -o kennedy_centro.pbf centro-latest.osm.pbf w/name=*ennedy
rm centro-latest.osm.pbf
wget https://download.geofabrik.de/europe/italy/isole-latest.osm.pbf
osmium tags-filter -o kennedy_isole.pbf isole-latest.osm.pbf w/name=*ennedy
rm isole-latest.osm.pbf
wget https://download.geofabrik.de/europe/italy/nord-est-latest.osm.pbf
osmium tags-filter -o kennedy_nord-est.pbf nord-est-latest.osm.pbf w/name=*ennedy
rm nord-est-latest.osm.pbf
wget https://download.geofabrik.de/europe/italy/nord-ovest-latest.osm.pbf
osmium tags-filter -o kennedy_nord-ovest.osm.pbf nord-ovest-latest.osm.pbf w/name=*ennedy
rm nord-ovest-latest.osm.pbf
wget https://download.geofabrik.de/europe/italy/sud-latest.osm.pbf
osmium tags-filter -o kennedy_sud.osm.pbf sud-latest.osm.pbf w/name=*ennedy
rm sud-latest.osm.pbf
osmium merge kennedy_centro.pbf kennedy_isole.pbf kennedy_nord-est.pbf kennedy_nord-ovest.osm.pbf kennedy_sud.osm.pbf -o kennedy_italy.pbf
rm kennedy_centro.pbf
rm kennedy_isole.pbf
rm kennedy_nord*
rm kennedy_sud*
ogr2ogr -f GeoJSON kennedy_points.geojson kennedy_italy.pbf points
ogr2ogr -f GeoJSON kennedy_lines.geojson kennedy_italy.pbf lines
ogr2ogr -f GeoJSON kennedy_multipolygons.geojson kennedy_italy.pbf multipolygons
ogr2ogr -f GeoJSON kennedy_multilinestrings.geojson kennedy_italy.pbf multilinestrings
ogr2ogr -f GeoJSON kennedy_other_relations.geojson kennedy_italy.pbf other_relations
``` 



