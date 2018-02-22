---
title:  "Handling KMLs for Web GIS"
date:   2017-10-7 20:00:00
categories: Web Application
tags: GIS, JavaScript, Web Application
---

When it comes to handling KMLs in Web GIS, it is always a conundrum for me. Let
me explain. ArcGIS API has this `KMLLayer` thing which is so simple to use but it
must take a KML url. So if a user wants to use a KML file to show their spatial
objects, he needs to upload his KML somewhere before adding a `KMLLayer` layer.

So, is there an option to show KMLs on a web app as easy as it is when someone
drags a KML to Google Earth and let the feature show. A do-able but time-consuming
way to achieve this is to create our own KML parser. After parsing the KML, we can
even have more flexibility to handle those KML-formatted spatial objects.
We can add them as whatever layers we want, depending on data type.

Here is some practice I made. In my case, I compared two ways of handling a KML
file that contains an `overlay` tag.   

Demo 1 - Using [`KMLLayer`](https://developers.arcgis.com/javascript/3/jsapi/kmllayer-amd.html)
![](/blog/images/demo/kml-by-url.gif)


Demo 2 - Using my own KML parser
![](/blog/images/demo/kml-google.gif)
