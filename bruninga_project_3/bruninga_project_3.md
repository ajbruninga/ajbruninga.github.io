---
A.J. Bruninga
---
GES 486 Project 3
---
12/19/18
---




### Maps

![Alt Text](https://github.com/ajbruninga/ajbruninga.github.io/blob/master/bruninga_project_3/md_fm_hex.png)


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
