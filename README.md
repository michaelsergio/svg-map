svg-map
=======

A polymer based map that can use existing SVG maps.

# Polymer Starter Project

This project includes a set of Polymer components and a starter project,
designed to be used with the [Polymer tutorial](http://polymer-project.org/docs/start/tutorial/intro.html).

In this tutorial, you build a simple client for `unquote`, the read-only social networking service.


## Project contents

 -   `starter`. Scaffolding for the starter project. If you're working through the tutorial, start here!
 -   `step-1` to `step-3`. Intermediate versions of the project. Check your work!
 -   `finished`. The completed `unquote` app.
 -   `components`. Selection of Polymer elements used in the project.
 -   `post-service`. A pre-built element that implements an interface to the `unquote` service. 
 -   `api`. Data for the the `unquote` service.
 -   `images`. Avatar images.

Find a problem in the tutorial? Please open a [Doc bug](https://github.com/Polymer/docs/issues/new) so we can fix it.

SVG-Map specific stuff
============================

Running
------------
To Run:
    python -m SimpleHTTPServer #python 2
    python -m http.server  # python 3

Map Sources
----------------
http://en.wikipedia.org/wiki/Wikipedia:Blank_maps

Usage Notes 
---------------

# I should be able to click on a glowing country and have a callback function appear.
    
    map.onclick(cc, status)
Not sure if cc should be reversed translated, or the id of the place clicked on.


    <svg-map>
        <glow color=blue cc=us></glow>
        <glow color=red cc=ru></glow>
    </svg-map>
Background color of ocean?

# Include a translations for CountryCode2 and CountryCode3.
ISO_3166-1_alpha-3
ISO_3166-1_alpha-2
Need to map countryCode to what id is on map.
For Example:
    CountryCode3 usa on north hempisphere map needs to be preprocessed into gUSA

Questions
===========
Should I have both id and cc as an option?
Maybe keep an internal lookup table mapping the two?

Can I transclude SVG functions into the svg-map for doing path, points, and labels?

How do I add translation functions? 
The answer is probably here:
http://www.polymer-project.org/docs/polymer/polymer.html

Add a tags element, which provides metadata for a given id or cc.
That way I can declaratively define affiliations.
<glow cc="US" tags="nato usa"></glow>
<glow cc="CH" tags="cowardly-neutral"></glow>
<glow cc="RU" tags="warsaw"></glow>
<glow cc="DE" tags="nato warsaw"></glow>
I can dynamically generate a legend from these tags.
Maybe also dynamically style them as well:
    if usa  in country.tags => return blue
    if nato and warsaw in country.tags => return yellow
    if nato in country.tags => return cyan

Have a batch update method for performance reasons. 
It should delay the update until all element transformations are done.

Mouse-over event - glow country
Click event - display factbook info

Maybe rename glow to country?

I should be able to do both:
    country.tags()
    getCountriesForTags("nato")
I think I need to implement a bimap to do that.
Install it into component folder.
https://github.com/alethes/bimap

Examples
============
Cold war example
------------------

    <svg-map src="world-map.svg">
        <glow color=blue   cc=us></glow>
        <glow color=red    cc=ru></glow>
        <glow color=cyan   cc=gb></glow>
        <glow color=pink   cc=ro></glow>
        <glow color=yellow cc=de></glow>
        <glow color="lightblue" cc=ocean></glow>
    </svg-map>

    // This one needs a translation function for USA -> gUSA
    <svg-map src="northen-hempisphere.svg">
        <glow color=blue   cc=USA></glow>
        <glow color=red    cc=RUS></glow>
        <glow color=cyan   cc=GBR></glow>
        <glow color=pink   cc=ROU></glow>
        <glow color=yellow cc=DEU></glow>
    </svg-map>    

Clicking on any one will display the statistics of the country.

Fact Book Lookup
---------------------
    <svg-map src="world-map.svg">
        <glow color="lightblue" cc=ocean></glow>
    </svg-map>

Entirely JS Driven.
Show dropdown box with countries of world.
Have JSON Data live in seperate file.
Render data.

Embed another polymer project to render flag icons for cc2 
stevenrskelton/flag-icon


Coolest Flight Path
--------------------
    <svg-map src="world-map.svg">
        <glow color=green cc=us></glow>
        <glow color=green cc=ae></glow>
        <glow color="lightblue" cc=ocean></glow>
        <marker label="San Francisco" point="XXX,YYY"></marker>
        <marker label="Dubai" point="XXX,YYY"></marker>
        <!-- Eye-balled approximation -->
        <path style="dashed" path="XXX,YYY, XXX,YYY"></path>
    </svg-map>

    <svg-map src="northen-hempisphere.svg">
        <glow color=green cc=us></glow>
        <glow color=green cc=ae></glow>
        <marker label="San Francisco" point="XXX,YYY"></marker>
        <marker label="Dubai" point="XXX,YYY"></marker>
        <!-- Eye-balled approximation -->
        <path style="dashed" path="AAA,BBB, AAA,BBB"></path>
    </svg-map>


This draws a path from San Francisco to Dubai over the Arctic on flight number ??

