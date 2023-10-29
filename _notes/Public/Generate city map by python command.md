---
title: Generate city map by python command
feed: show
date : 29-10-2023
---

Jeśli marzyłeś kiedyś o stworzeniu pięknego plakatu bazując na mapie Twojego miasta lub z jagiekolwiek podowu potrzebujesz nieszablonowej mapy.

Istnieje prosty sposób na stworzenie wspaniałej mapy oparte na zarysie budynków 



W tym celu należy wykorzystać bibliotekę:
https://github.com/gboeing/osmnx

oraz dokumentacji

https://osmnx.readthedocs.io/en/stable/index.html


która pozwala na generowanie obrazów na zadaną konfigurację

oraz 
https://github.com/ipython/ipython

pozwalający zapisać wszystko do pliku



```
import osmnx as ox, geopandas as gpd
from IPython.display import Image

ox.config(log_console=True, use_cache=True)
ox.config(log_file=True, log_console=True, use_cache=True)
img_folder = 'images'
extension = 'png'
size = 100000

# configure the inline image display
img_folder = "images"
extension = "png"
size = 240

# specify that we're retrieving building features from OSM
tags = { "building": True }
gdf = ox.features_from_place("New York, USA", tags)
gdf_proj = ox.project_gdf(gdf)
fp = f"./{img_folder}/piedmont_bldgs.{extension}"
fig, ax = ox.plot_footprints(
    gdf_proj, 
    filepath=fp, 
    dpi=1600, 
    bgcolor='#ffffff', 
    color='#000000',
    save=True, 
    show=False, 
    close=True
    )
Image(fp, height=size, width=size)
