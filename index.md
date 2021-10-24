---
title: "P5.js - Art"
date: 2021-10-22T20:53:27+02:00
draft: false
toc: true
headercolor: "teal-background"
taal: Javascript 
---

Kunst maken in de browser.

<!--more-->

## Introductie

Naast kunst met [Scratch](/instructies/scratch-art/) en [Python](/instructies/python-art/), kun je ook kunst 
programmeren met [Processing](https://processing.org/).

Er is ook een Processing variant voor in de browser. Deze heet [p5.js](https://p5js.org/). We gaan er in deze instructie
mee aan de slag. Eerst een voorbeeld van wat je ermee kunt doen:
<div id="sketch-holder">
<script src="p5.js-widget/p5.js_0.4.23/p5.js"></script>
<script src="sketch.js"></script>
</div>
{{< voorbeeld kop="de code bij dit voorbeeld" >}}
<p>Favoriet van Jaap! 😉</p>
<p>Kopie van <a href="https://openprocessing.org/sketch/422446">Sketch 422446</a>.
{{< highlight javascript "linenos=table,linenostart=1" >}}
var circle = 200;
var rot;
var col;
var freq = 0.000005;
var cont = 0;
var r;

function setup() {
    createCanvas(600, 600);
}

function draw() {
    background(242);
    translate(300, 300);
    rotate(radians(rot));
    
    ellipseMode(RADIUS);
    for (var i=0; i<500; i ++) {
        circle= 200 + 50*sin(millis()*freq*i);
        col=map(circle,150,250,255,60);
        r=map(circle,150,250,5,2);
        fill(col,0,74);
        noStroke();
        ellipse(circle*cos(i), circle*sin(i),r,r);
        rot=rot+0.00005;
    }
}
{{< /highlight >}}
{{< /voorbeeld >}}

### Editor

p5.js is een Javascript bibliotheek. Deze kun je in elke editor gebruiken. Door een webserver te gebruiken, kun je het
resultaat bekijken in een webbrowsers. Het is echter makkelijker om een editor in de browser te gebruiken. Ga
daarvoor naar <a href="p5.js-widget/p5-widget.html" target="_blank">deze editor</a>.

De volgende instructies en voorbeelden gaan ervan uit dat je deze editor gebruikt.

## De basis

p5.js scripts hebben de volgende basis:

{{< highlight javascript "linenos=table,hl_lines=1-2 4-5,linenostart=1" >}}
function setup() {
}

function draw() {
}
{{< /highlight >}}

Er zijn twee functies die worden aangeroepen door de p5.js bibliotheek:

- `setup()` wordt éénmaal bij de start van het script uitgevoerd
- `draw()` wordt oneindig herhaald en iedere schermvernieuwing aangeroepen (normaal 60 keer per seconde)

In de `setup()` functie zet je éénmalige instellingen, zoals bijvoorbeeld een vaste achtegrondkleur. In de `draw()`
functie dingen die veranderen, zoals bijvoorbeeld een verschuivende kubus.

Het volgende voorbeeld tekent een draaiend vierkant:

{{< highlight javascript "linenos=table,hl_lines=2 6-9,linenostart=1" >}}
function setup() {
    createCanvas(300, 300);
}

function draw() {
    background(255);
    translate(width / 2, height / 2);
    rotate(frameCount/50);
    rect(-26, -26, 52, 52);
}
{{< /highlight >}}




{{< licentie rel="http://creativecommons.org/licenses/by-nc-sa/4.0/">}}
