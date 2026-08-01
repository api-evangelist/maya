---
title: "AutoCAD 2027 Drag-Drop Fixed in Update 1"
url: "https://blog.autodesk.io/autocad-2027-drag-drop-fixed-in-update-1/"
date: "2026-07-28"
author: "Madhukar Moogala"
feed_url: "https://blog.autodesk.io/feed/"
---
When AutoCAD 2027 was first released with .NET 10 support, many developers encountered a critical regression: drag-and-drop operations from custom palettes to the drawing area would crash with an InvalidCastException. System.InvalidCastException: Unable to cast COM object of type 'System.__ComObject' to interface type 'System.Windows.Forms.IDataObject'. QueryInterface call failed with E_NOINTERFACE (0x80004002).
