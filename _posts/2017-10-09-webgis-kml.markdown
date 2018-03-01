---
title:  "Handling KMLs for Web GIS"
date:   2017-10-7 20:00:00
categories: Web Application
tags: GIS, JavaScript, Web Application
---

Here is some practice I made to load KMLs in Web GIS. In my case, I compared two ways of handling a KML
file that contains a KML `overlay` tag.   

Demo 1 - Using ArcGIS [`KMLLayer`](https://developers.arcgis.com/javascript/3/jsapi/kmllayer-amd.html)

What I like about: dead easy

What I dislike about: KMLs need to be uploaded somewhere before adding as a `KMLLayer` layer.

![](/blog/images/demo/kml-by-url.gif)



Demo 2 - Using my own KML parser

What I like about: I can just drag in my KMLs from local; more flexibility of handling KML-formatted spatial objects

What I dislike about: I have to test with loads of KMLs in order to get a robust parser
![](/blog/images/demo/kml-google.gif)
