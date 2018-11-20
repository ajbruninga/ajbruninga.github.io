---
A.J. Bruninga
---
GES 486 Project 2
---

For this project I decided to look at the expansion of vacant buildings in Baltimore City
and to see if they had any effect on where Econview Projects were constructed. I got my data from the Baltimore City Open GIS Portal and used a State Plane projection. First I had to deal with a formatting issue on the Vacant Buildings layer because it had the dates as mmddyy and the year could not be easily used until it was extracted. With the note year available, I was able to use python to select out each year's vacant buildings data, save them as separate layers, and change some symbology. I then did a Count Points in Polygon of the vacant buildings per year for each council district. Making a GIF out of five years of the data was a good way to illustrate the increase in vacant buildings over time.

The more interesting part of my project came next as I analyzed the possible relationship between vacant buildings and econview projects. In order to find out how many vacant buildings were within a half-mile of each econview project, I made a half-mile radius heatmap on the vacant buildings. I then used the SAGA tool "add raster values to points" to extract the heatmap values at each econview project. While this method provided a reasonable assessment, in hindsight I think a simple intersection of a half-mile buffer around each econview project would have given a more accurate count of vacant buildings nearby. My heatmap method under-projected the number of vacant buildings within a half-mile because the value of the heatmap raster decreased from 1 at the vacant building point to zero at the surrounding ring a half-mile away. This resulted in most vacant buildings near econview projects being added as fractions in the raster rather than a true count. Still, while the actual numbers may be low, the ratios between econview projects should remain unchanged.



### Maps

![Alt Text](https://github.com/ajbruninga/ajbruninga.github.io/blob/master/VB_CD_201317.gif)


![Alt Text](https://github.com/ajbruninga/ajbruninga.github.io/blob/master/EPD_VB_201317.gif)


There were relatively few econview projects near concentrations of vacant buildings, with as few as 9% and at most 32% of econview projects within a half-mile of 10 vacant buildings. Instead, there were a higher concentration of econview projects in the downtown area where there were few vacant buildings.


### My Code
```python
from qgis.utils import iface
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.core import *
import processing


cd = iface.addVectorLayer('Z:/ges486/Project_2/shapefiles/Council_District.shp', 'Council_District', 'ogr')
VB_200818 = iface.addVectorLayer('Z:/ges486/Project_2/shapefiles/VB_200818.shp', 'VB_200818', 'ogr')
EPD_200818 = iface.addVectorLayer('Z:/ges486/Project_2/shapefiles/EPD_200818.shp', 'EPD_200818', 'ogr')

renderer = cd.renderer()
symbol = renderer.symbol()
symbol.setOpacity(0.25)

VB_200818.selectByExpression("NOTE_YEAR = 2013")
QgsVectorFileWriter.writeAsVectorFormat(VB_200818, 'Z:/ges486/Project_2/shapefiles/VB_2013p.shp', 'utf-8', VB_200818.crs(), 'ESRI Shapefile', True)
VB_2013 = iface.addVectorLayer('Z:/ges486/Project_2/shapefiles/VB_2013p.shp', 'VB_2013p', 'ogr')

EPD_200818.selectByExpression("CSYear = 2013")
QgsVectorFileWriter.writeAsVectorFormat(EPD_200818, 'Z:/ges486/Project_2/shapefiles/EPD_2013p.shp', 'utf-8', EPD_200818.crs(), 'ESRI Shapefile', True)
EPD_2013 = iface.addVectorLayer('Z:/ges486/Project_2/shapefiles/EPD_2013p.shp', 'EPD_2013p', 'ogr')

sym = QgsMarkerSymbol.createSimple({'name':'circle', 'color':'blue', 'size':'1'})
rend = VB_2013.renderer()
rend.setSymbol(sym)
sym.setOpacity(0.5)
```
