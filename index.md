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

<script src="p5.js-widget/p5.js_0.4.23/p5.js"></script>
<script src="sketches.js"></script>

## Introductie

Naast kunst met [Scratch](/instructies/scratch-art/) en [Python](/instructies/python-art/), kun je ook kunst 
programmeren met [Processing](https://processing.org/).

Er is ook een Processing variant voor in de browser. Deze heet [p5.js](https://p5js.org/). We gaan er in deze instructie
mee aan de slag. Eerst een voorbeeld van wat je ermee kunt doen:

<div id="demo"></div>

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
resultaat bekijken in een webbrowser. Het is echter makkelijker om een editor in de browser te gebruiken. Ga
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
    createCanvas(150, 150);
}

function draw() {
    background(255);
    translate(width / 2, height / 2);
    rotate(frameCount/50);
    rect(-26, -26, 52, 52);
}
{{< /highlight >}}
<div class="p5js_voorbeeld" id="voorbeeld1"></div>

We zullen stap voor stap door de code heen lopen:

 * op regel 2 in de `setup` functie wordt het tekenblad (canvas) gemaakt. Dit hoeft slechts 1 keer te gebeuren.
 * regels 6 tot en met 9 worden telkens herhaald:
   * `background(255)` maakt de achtergrond kleur wit (waarde 255).
   * `translate(width / 2, height / 2)` zorgt ervoor dat het vierkant midden in het tekenblad komt.
   * `rotate(frameCount / 50)` draait het vierkant iedere keer dat dit wordt uitgevoerd. `frameCount` staat voor het
     aantal schermvernieuwingen per seconde. Daardoor bepaald `frameCount / 50` de snelheid waarmee het vierkant draait.
   * tenslotte tekent `rect(-26, -26, 52, 52)` het vierkant.

**Opdracht 1**: neem de code over in de editor en kijk of er een draaiend vierkant wordt getekend door op de speel knop
    te klikken.  
**Opdracht 2**: vervang waarde 255 op regel 6 eens met een andere waarde tussen 0 en 256. Wat gebeurt er met een lage
    waarde? En wat met een hoge?  
**Opdracht 3**: misschien vraag je je af waarom de achtergrond iedere keer opnieuw moet worden getekend? Door `//` voor
    de regel te zetten, maak je er commentaar van en wordt het niet meer uitgevoerd. Zet `//` voor regel 6. Wat gebeurt
    er?  
**Opdracht 4**: regel 8 zorgt ervoor dat het vierkant draait. Verander waarde 50 eens door 10. Wat gebeurt er? En bij
    een waarde van 100?  
**Opdracht 5**: regel 9 tekent het vierkant. De eerste twee getallen -26 verschuiven het draaipunt van het vierkant
    horizontaal en vertikaal. De twee laatste bepalen de hoogte en breedte. Vervang de getallen 52 eens door 75. Wat
    gebeurt er? En als je één van de twee 52 laat en de ander veranderd naar 75?

Na het uitvoeren van deze eerste opdrachten begrijp je een beetje hoe het werkt. In de volgende hoofdstukken gaan we 
verder met meer voorbeelden en uitleg.

## Cirkels en muis

In dit hoofdstuk gaan we kunst maken met je muis. Beweeg je muis maar eens over het grijze vlak hieronder. 😉
<div class="p5js_voorbeeld" id="voorbeeld2"></div>
Stap voor stap gaan we dit nabouwen.

### Een cirkel


{{< licentie rel="http://creativecommons.org/licenses/by-nc-sa/4.0/">}}
