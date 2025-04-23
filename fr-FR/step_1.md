Les images peuvent avoir des tailles de fichier volumineuses.

Quand une page web se charge, toutes les images sont chargées et cela peut utiliser beaucoup de bande passante.

Tu peux améliorer les performances du navigateur en ne chargeant que les images quand elles sont nécessaires.

Voici un exemple d'images à chargement à lent :

![Un gif montrant des images en cours de chargement alors qu'elles entrent dans la fenêtre d'affichage du navigateur](images/background-attachment-fixed.gif)

Voici comment cela se fait :

**1 - Ajouter un nouvel attribut à chaque élément d'image**

Dans ton/tes fichier(s) HTML ajoute un attribut `data-src` à chaque élément `<img>`, et définis la valeur de l'attribut à l'image que tu veux charger.

Définis l'attribut `src` pour chaque élément `<img>` à un fichier image (ou animation/gif).

Voici un exemple :

## --- code ---

language: html
filename:
line_numbers: false
line_number_start:
line_highlights:
-----------------------------------------------------

<img src="spinner.gif" data-src="snail.svg" />

\--- /code ---

**2 - Utiliser l'Intersection Observer**

Crée un Intersection Observer JavaScript pour observer chaque élément de l'image et, si une image entre dans la fenêtre d'affichage, change la valeur de son attribut `src` à la valeur de son attribut `data-src` (le fichier image que tu veux charger).

Tu peux utiliser JavaScript pour observer chaque élément `<img>`.

Voici un exemple du projet [Histoire animée](https://projects.raspberrypi.org/en/projects/animated-story) dans le parcours [Plus de web](https://projects.raspberrypi.org/en/raspberrypi/more-web) :

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