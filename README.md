# CSS to the Rescue

## Inhoudsopgave
- De opdracht
- Omschrijving
- Onderzoek/Leermomenten
- Eindresultaat
- Conclusie

## De Opdracht
De opracht die ik heb gekozen is het maken van een vuurwerkshow met CSS. Hierbij is het de bedoeling om een 'show' met effecten en interactie te maken waarme je onderzoek doet naar de functies van tegenwoordig CSS.

## Omschrijving
Ik heb van te voren (expres) geen plan gemaakt van hoe mijn show er uit gaat zien. 
Mijn intentie is het ondekken van nieuwe functies en het spelen met CSS en vanuit hier iets samenvoegen en opleveren.

## Onderzoek
Hieronder volgt alles wat ik onderzocht heb, ik heb gekeken naar zoveel mogelijk dingen waar ik nog niet zo veel of helemaal geen ervaring mee had en hier ben ik mee gaan expirimenteren, een functie hoeft het niet te hebben, als het er maar leuk uitziet.

### Box shadow colors
Ik ben begonnen naar onderzoek doen naar box shadows in combinatie met kleuren, ik heb gekeken naar hoe ik een mooi effect kon combineren met mooie shadows.
<img width="1432" alt="outline glow " src="https://user-images.githubusercontent.com/24406793/223713804-96f62935-7008-4f54-80cc-77895d505768.png">
<img width="1432" alt="box shadow" src="https://user-images.githubusercontent.com/24406793/223711812-779c821e-ccd2-452c-83c5-254c262aca02.png">

```CSS
   box-shadow: 
    inset 0 0 50px #fff,      /* inner white */
    inset 20px 0 80px #f0f,   /* inner left magenta short */
    inset -20px 0 80px #0ff,  /* inner right cyan short */
    inset 20px 0 300px #f0f,  /* inner left magenta broad */
    inset -20px 0 300px #0ff, /* inner right cyan broad */
    0 0 50px #fff,            /* outer white */
    -10px 0 80px #f0f,        /* outer left magenta */
    10px 0 80px #0ff;         /* outer right cyan */
    
```

Hier ben ik vervolgens verder mee gegaan om een mooi hovereffect te krijgen. (niet erg nuttig, wel mooi)
![ezgif com-video-to-gif-2](https://user-images.githubusercontent.com/24406793/223712866-a88abc15-9965-4023-bcf3-80808c50c3f8.gif)

Door een transition te zetten op de box shadow die word getriggerd door hover krijg je dit effect.

### Checkbox en has() selector
Ik heb onderzoek gedaan naar het stylen van checkboxes, die erg van pas kunnen komen bij een vuurwerkshow. 
![checkbox](https://user-images.githubusercontent.com/24406793/223713966-a74d213e-fab9-4d3b-b605-7ef71e47e28f.gif)

Om een checkbox te kunnen stylen moet je eerst zorgen dat de originele checkbox niet getoond word, dit kan op meerdere manieren, ik heb display: none gebruikt.
```CSS
main form input {
  display: none;
} 

main form label {
  position: absolute;
  bottom: 0;
  display: block;
  transition: .5s;
  height: 4em;
  width: 10em;
  border-radius: 0%;
  background-color: red;
}

main form label:hover {
  cursor: pointer;
}

body :has(#check:checked) h1 {
  color: red;
}

#check:checked + label {
  height: 5em;
  width: 5em;
  border-radius: 50%;
  background-color: forestgreen;
  bottom: 50%;
  left: 2.5em;
}

```

### has() selector 
Met de has() selector kan je stylen buiten de parent om, iets wat voorheen nog niet mogelijk was. Ik vind dit nu nog vrij ingewikkeld maar dit is enorm interessant, het lijkt op een if else statement in CSS.

![ezgif com-video-to-gif-3](https://user-images.githubusercontent.com/24406793/223715322-31b0fdde-e6b8-4fd0-8aaa-ec75d61a66fa.gif)

```CSS

label {
	cursor: pointer;
	width: 200px;
	height: 100px;
	background: #BDCEE7;
	display: block;
	border-radius: 100px;
	position: relative;
 box-shadow: 
  inset 2px 2px 3px 1px rgba(0, 0, 0, 0.2);
  margin-left: 5%;
}
label:before {
  width: 80px;
  content: "";
  height: 80px;
  background-color: rgb(255, 255, 255);
  position: absolute;
  top: 10px;
  left: 10px;
  border-radius: 100px;
  transition: .5s;
}

/* eerst de normale styling van de checkbox uitzetten */
input[type=checkbox]{
	height: 0;
	width: 0;
	appearance: none;
}

label:has(input:checked)::before {
  transform: translateX(100px);
}
label:has(input:checked) {
  background-color: rgb(93, 158, 92);
}

```

### CSS motion path
Met CSS motion path kan je objecten laten bewegen volgens een bepaalde route. Om dit te doen heb je een path nodig (bijvoorbeeld die van een SVG), en kan je vervolgens via een animatie het object over dit pad laten bewegen.

![ezgif com-video-to-gif-4](https://user-images.githubusercontent.com/24406793/223716956-0ec5c834-41b2-4aeb-ad04-5342d204d37c.gif)

```CSS 
offset-path: path("M135.924 694.089C135.924 675.565 137.177 657.724 128.758")
animation: move 3000ms infinite ease-in-out; 

@keyframes move {
  0% {
    
    offset-distance: 0%;
  }

  100% {
  offset-distance: 80%;
  
  }
} 
```

### gradient effect
![ezgif com-video-to-gif-5](https://user-images.githubusercontent.com/24406793/223718938-c73bd2eb-1a15-40ab-891c-fb16a44f54aa.gif)
```CSS
div {
	width:2em;
	aspect-ratio:1;
	
/* 	background-color:red; */
	border-radius:50%;
	
	background-image:
		radial-gradient(
			closest-side,
			transparent calc(100% - var(--size, 2em)),
			var(--color, blue) 100%
		);
	
	transition:.2s --size, .2s --color, .2s width;
}

div:hover {
	--color:red;
	--size:4em;
	
	width:20em;
}

@property --color {
  syntax: "<color>";
  inherits: false;
  initial-value: blue;
}
```


Dit zijn de hoofdonderdelen die ik onderzocht heb in de afgelopen 3.5 week. Natuurlijk heb ik nog veel meer geleerd maar dit zijn de hoofdpunten, nu is het een kwestie van alles samenvoegen en combineren, en kijken wat hier uit kan komen.

##Eindresultaat

![ezgif com-video-to-gif-6](https://user-images.githubusercontent.com/24406793/223719958-e9402f33-dc45-4bc9-8484-fc6083c27230.gif)

Het eindresultaat is een combinatie van mijn onderzochte doelen, ik heb de raket die opstijgt gradients gegeven, laten ontploffen in cirkels met gradients en shadows, bewegende wolken toegevoegd en met de has selector de animaties van de raket aangezet.

```CSS

body:has(.checkbox:checked) section:first-of-type ul li:nth-of-type(2) {
  animation: mainshadow 5000ms infinite; 
}
body:has(.checkbox:checked) section:first-of-type ul {
  animation: move 5000ms infinite ease-in-out;
}
body:has(.checkbox:checked) section:first-of-type ul li:nth-of-type(2)::after {
  animation: aftershadow 5000ms infinite; 
}

body:has(.checkbox:checked) section:first-of-type ul li:nth-of-type(2)::before {
  animation: beforeshadow 5000ms infinite; 
}

body:has(.checkbox:checked) section:first-of-type ul li:nth-of-type(3) {
  animation: explode1 5000ms infinite;
}
body:has(.checkbox:checked) section:first-of-type ul li:nth-of-type(4) {
  animation: explode2 5000ms infinite;
}
```

##Conclusie
CSS kan een heel stuk meer dan dat ik voor dit project dacht, ik zou voor minimaal de helft van alle effecten Javascript gebruiken, terwijl dit nergens voor nodig is. Ik ben redelijk tevreden met het eindresultaat, en tevreden met het onderzoek. Ik heb erg veel geleerd over CSS en ik zal nu ook in de toekomst in de gaten houden wat voor nieuwe dingen er komen. 

