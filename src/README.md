# OpenLayers Workshop

Welcome to the **OpenLayers 3 Workshop**. This workshop is designed to give you a comprehensive overview of OpenLayers as a web mapping solution.

## Setup

You will need:

* a text editor like Atom, Brackets, Sublime Text, Texmate (Mac only), Gedit (Linux only), Notepad++ (Windows only)

* a web server

For this second case, you can follow below instructions.


Assuming you already have an installed Python or Node

With Python, you can run a local webserver by changing the root of the repository in a command prompt and running:

    python -m SimpleHTTPServer

If you have Node installed, install `http-server` with the command `npm install http-server`. Then, change the rpository root and run:

    http-server


These instructions assume that you are starting with an `openlayers-workshop.zip` archive from the latest [workshop release](https://github.com/openlayers/workshop/releases).  In addition, you'll need [Node](https://nodejs.org/) installed to run a development server for the OpenLayers library.

This will start a development server where you can read the workshop documentation and work through the exercises: {{ book.workshopUrl }}.

## Overview

This workshop is presented as a set of modules.  In each module you will perform a set of tasks designed to achieve a specific goal for that module.  Each module builds upon lessons learned in previous modules and is designed to iteratively build up your knowledge base.

The following modules will be covered in this workshop:

* [Basics](basics/README.md) - Learn how to add a map to a webpage with OpenLayers.
* [Layers and Sources](layers/README.md) - Learn about layers and sources.
* [Controls and Interactions](controls/README.md) - Learn about using map controls and interactions.
* [Vector Topics](vector/README.md) - Explore vector layers in depth.
