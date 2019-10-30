# 1. BUILD
`docker build .   -t nominatim   --build-arg BUILD_THREADS=8   --build-arg BUILD_MEMORY=16GB   --build-arg OSM2PGSQL_CACHE=14000   --build-arg RUNTIME_THREADS=8   --build-arg RUNTIME_MEMORY=16GB   --build-arg PBF_URL=https://download.geofabrik.de/europe/netherlands/zuid-holland-latest.osm.pbf  --build-arg POSTGIS_VERSION=2.5  --build-arg PGSQL_VERSION=9.6`

# 2. SAVE
`docker save nominatim -o nominatim-docker`

# 3. LOAD
`docker image load -i nominatim-docker`

# 4. RUN
`docker run --restart=always -d -p 8080:80 --name=nominatim -h nominatim nominatim`

# 5. RUN BASH
`docker exec -it nominatim bash`

# 6. EDIT
`Adjust url for tiles and hostname
vi /srv/nominatim/Nominatim/settings/defaults.php
vi /srv/nominatim/Nominatim/build/settings/settings.php
 
#@define('CONST_Map_Tile_URL', '[https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png]https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png');
@define('CONST_Map_Tile_URL', 'http://nominatim/osm_tiles/{z}/{x}/{y}.png');`

# 7. RESTART
docker restart nominatim