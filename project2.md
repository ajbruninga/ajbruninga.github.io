---
A.J. Bruninga
---
GES 486 Project 2
---

For this project I decided to look at the relationship between Econview Project
Data for Baltimore City and the proximity of vacant buildings.

### Maps

!VB_CD_201317.gif

[https://github.com/ajbruninga/ajbruninga.github.io/blob/master/EPD_VB_201317.gif]

EPD_VB_201317.gif


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
