Afbeeldingen kunnen grote bestandsgroottes hebben.

Wanneer een webpagina wordt geladen, worden alle afbeeldingen geladen en dit kan veel bandbreedte gebruiken.

Je kunt de prestaties van jouw browser verbeteren door afbeeldingen alleen te laden wanneer dat nodig is. Dit staat bekend als 'lazy loading'.

Hier is een voorbeeld van het traag laden van een aantal afbeeldingen:

![Een gif die afbeeldingen laat zien die worden geladen op het moment dat ze in de viewport van de browser verschijnen.](images/background-attachment-fixed.gif)

Dit is hoe het gedaan wordt:

**1 - Voeg een nieuw kenmerk toe aan elk afbeeldingselement**

Voeg in je HTML-bestand(en) een `data-src`-kenmerk toe aan elk `<img>`-element en stel de kenmerkwaarde in op het afbeeldingsbestand dat je wilt laden.

Stel het `src`-kenmerk voor elk `<img>`-element in op een tijdelijke afbeelding (of spinneranimatie/gif).

Hier is een voorbeeld:

--- code ---
---
language: html
filename: 
line_numbers: false
line_number_start: 
line_highlights:
---

<img src="spinner.gif" data-src="snail.svg" />

--- /code ---

**2 - Gebruik de intersection observator**

Maak een JavaScript-intersectieobservator om elk afbeeldingselement te observeren en, als de afbeelding in de viewport verschijnt, de waarde van het `src`-kenmerk te wijzigen in de waarde van het `data-src`-kenmerk (het afbeeldingsbestand dat je wilt laden).

Je kunt JavaScript gebruiken om elk `<img>` element te observeren.

Hier is een voorbeeld van het project [Geanimeerd verhaal](https://projects.raspberrypi.org/nl-NL/projects/animated-story) in het pad [Meer web](https://projects.raspberrypi.org/nl-NL/raspberrypi/more-web):

--- code ---
---
language: js
filename: 
line_numbers: true
line_number_start: 1
line_highlights:
---

const lazyImages = document.querySelectorAll("img");
const imageObserver = new IntersectionObserver((entries) => {
  entries.forEach(
    (entry) => {
      if (entry.isIntersecting) {
        entry.target.src = entry.target.getAttribute("data-src");
        imageObserver.unobserve(entry.target);
      }
    }
  );
});
lazyImages.forEach((lazyImage) => imageObserver.observe(lazyImage));

--- /code ---