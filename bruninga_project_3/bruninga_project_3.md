---
A.J. Bruninga
---
GES 486 Project 3
---
12/19/18
---


My goal for this project was to make a map showing the location and density of farmers' markets in Maryland. My question was then to determine the best farmers' markets in the state by calculating their proximity to agricultural land. Theoretically the best markets would be those closest to the farms themselves. I got my data from the Maryland GIS Open Data Catalog (http://data.imap.maryland.gov/) and used a WGS 84 projection for the first map and a MD State Plane projection for the 3D map. 

For my first map showing the locations and densities of farmers' markets in Maryland, I began by using some python (documented at bottom) to import the point data and a background county shapefile. I set some basic symbology in python like color and opacity. I then used the Create Grid tool in QGIS to create a 10 mile by 10 mile hexagonal grid over the state, which I clipped using the vector overlay Extract/Clip by Extent tool to fit the study area. To find the density of farmers' markets, I utilized the Count Points in Polygon processing tool to add a new field to the hexagon layer that contained the number of markets within each hexagon. After that, it was a simple matter of changing the symbology to graduated for best visual effect.


### Maps

![Alt Text](https://github.com/ajbruninga/ajbruninga.github.io/blob/master/bruninga_project_3/md_fm_hex.png)


My second map illustrates the best farmers' markets in the state based on the assumption that the best ones are those closest to the agricultural land where the crops originate. For this map I downloaded some additional data from the MD Open Data Catalog, namely the vector layer of Maryland Agricultural Designations - Priority Preservation Areas. I realize this doesn't represent all agricultural land in the state, but it was the only data available and it may be that preservation areas are the ones growing the kind of crops that are sold in farmers' markets. While I can offer no proof, it could be that the areas in need of preservation got to that point by selling a diversity of market crops rather than the probably more economically viable industrial cash crops.

Anyway, I made this map by using the Random Points Inside Polygons tool 

![Alt Text](https://github.com/ajbruninga/ajbruninga.github.io/blob/master/bruninga_project_3/md_fm_cnt.png)


### My Code
```python
from qgis.utils import iface
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.core import *
import processing


md_fm = iface.addVectorLayer('C:/Users/ajbru_000/Documents/UMBC/486/Project_3/shapefiles/md_fm_proj.shp', 'MD Farmers Markets', 'ogr')
md_counties = iface.addVectorLayer('C:/Users/ajbru_000/Documents/UMBC/486/Project_3/shapefiles/md_counties.shp', 'MD Counties', 'ogr')

sym = QgsMarkerSymbol.createSimple({'name':'circle', 'color':'blue', 'size':'0.4'})
rend = md_fm.renderer()
rend.setSymbol(sym)
sym.setOpacity(0.8)

renderer = md_counties.renderer()
symbol = renderer.symbol()
symbol.setColor(QColor(Qt.white))
symbol.setOpacity(0.5)
active_layer.triggerRepaint()
```
