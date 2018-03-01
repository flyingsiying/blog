---
title:  "Creating Customizable Symbology Function for Web GIS"
date:   2017-10-7 10:05:23
categories: Web Application
tags: GIS, JavaScript, Web Application
---


Creating a symbol editing window on the Web GIS Application simply mimics the
process of symbolozing a layer in ArcMap Desktop. Users can symbolize
feature layers in different ways depending on the type of data.

To summarize how I build this functionality:
* A dialog object is created in JavaScript to allow a user to enter different
settings, such as fill color or outline color.
* When a user clicks the save button, all the symbol settings will be saved as a
 configuration and attached to the layers.
* At the same time, a JavaScript function, `renderSymbology`, will be called to
render new symbols depending on render type.
* Another JavaScript function, `makeLegend`, will be called to fire any legend
changes.
* Last but not least, when a user reloads the application, layers will appear as
 how the user defines it to be from the last editing. `renderSymbology` and `makeLegend`
 functions were called again to generate the customized symbols by grabbing the updated
 symbol configuration that is attached to each layer.         


Demo 1 - Styling a [`SymbolMarkerSymbol`](https://developers.arcgis.com/javascript/3/jsapi/simplemarkersymbol-amd.html)
![](/blog/images/demo/webgis-symbol-marker.gif)


Demo 2 - Converting a [`SymbolMarkerSymbol`](https://developers.arcgis.com/javascript/3/jsapi/simplemarkersymbol-amd.html)
to a [`PictureMarkerSymbol`](https://developers.arcgis.com/javascript/3/jsapi/picturemarkersymbol-amd.html)
![](/blog/images/demo/webgis-symbol-picture.gif)


Demo 3 - Playing with [`UniqueValueRenderer`](https://developers.arcgis.com/javascript/3/jsapi/uniquevaluerenderer-amd.html)
![](/blog/images/demo/webgis-symbol-unique.gif)
