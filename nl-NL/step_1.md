Afbeeldingen kunnen grote bestandsgroottes hebben.

When a webpage loads, all the images are loaded and this can use lots of bandwidth.

You can improve browser performance by only loading images when they are needed. This is known as 'lazy loading'.

Here's an example of some lazy loading images:

![A gif showing images loading as they enter the browser's viewport.](images/background-attachment-fixed.gif)

Dit is hoe het gedaan wordt:

**1 - Voeg een nieuw kenmerk toe aan elk afbeeldingselement**

In your HTML file(s), add a `data-src` attribute to each `<img>` element, and set the attribute value to the image file you want to load.

Stel het `src`-kenmerk voor elk `<img>`-element in op een tijdelijke afbeelding (of spinneranimatie/gif).

Hier is een voorbeeld:

## --- code ---

language: html
filename:
line_numbers: false
line_number_start:
line_highlights:
-----------------------------------------------------

<img src="spinner.gif" data-src="snail.svg" />

\--- /code ---

**2 - Use the intersection observer**

Create a JavaScript intersection observer to observe each image element and, when the image enters the viewport, change the value of its `src` attribute to the value of its `data-src` attribute (the image file you want to load).

Je kunt JavaScript gebruiken om elk `<img>` element te observeren.

Here is an example from the [Animated story](https://projects.raspberrypi.org/en/projects/animated-story) project in the [More web](https://projects.raspberrypi.org/en/raspberrypi/more-web) path:

## --- code ---

language: js
filename:
line_numbers: true
line_number_start: 1
line_highlights:
-----------------------------------------------------

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

\--- /code ---
