---
title:  "ArcGIS REST Service Parser"
date:   2017-11-13 21:05:23
categories: Web Application
tags: GIS, Web Application, Java
---

ArcGIS REST Service Parser is an Oracle SQL-driven application I designed for managing published ArcGIS REST Services.

What is an ArcGIS REST Service?
An ArcGIS REST Service is a GIS Service published on an ArcGIS Service and considered a resource and can be access through a URL
such as https://basemap.nationalmap.gov/arcgis/rest/services/USGSTopo/MapServer (USGS). This URL is also known as REST endpoint.
Each ArcGIS REST Service usually has properties that describe it, operations that can be performed on it, and child resources.


How does my application work? It consists of two major parts - parsing and searching.

First, a user can parse in his service(s) by simply entering the service URL. This URL can be at the server level or the layer level.
He can also choose whether to create thumbnail images or assign a rank to his service(s). If the thumbnail option is chosen, the parsing process
would create an overview visualization for this service.  
![](/blog/images/demo/arcgis-rest-1.gif)


Then, a user can search any parsed services in the database by keywords.
![](/blog/images/demo/arcgis-rest-2.gif)


Last but not least, a user can click onto each search result to enter the Web GIS interface so that he could play around with the layer.
![](/blog/images/demo/arcgis-rest-3.gif)
