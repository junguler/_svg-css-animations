## svg animations
svgs are the most popular extension for vector images, unlike rastor images (jpg, png ...) vector images dont contain pixels but calculations of the shapes that make the final image

this makes them easier to scale without the quality loss and it usually makes them take smaller file size if you are working with simple shapes

<br>

## the basic layout of svg images
svgs are very easy to modify since they are made of calculations, if we open a svg file with a text editor you can see that it's actually really easy to understand

everything is inside tags `<>` with the `svg` tag containing everything, here is the code for a very simple svg image of a rectangle i quickly made in inkscape so we can take a look inside 
```
<svg width="47.404mm" height="21.129mm" version="1.1" viewBox="0 0 47.404 21.129" xmlns="http://www.w3.org/2000/svg">
<rect width="47.404" height="21.129" style="fill:#20a6ff;paint-order:markers fill stroke"/>
</svg>
```
![](examples/A-1.svg)

the svg tag contains the width and height of our image, note that this is the value you decided in your svg editor and can be easily changed, the reason for these to exist is so we can have a default value.

the rect tag here contains x coordinantes, width and height and some styling we applied in our svg editor (in my case inkscape)

note that this rect tag was created because i made a very simple rectangle image, if we make a more complex shape this tag changes depending the complexity, here is another example:
```
<svg width="48.157mm" height="45.893mm" version="1.1" viewBox="0 0 48.157 45.893" xmlns="http://www.w3.org/2000/svg">
<path transform="matrix(.26458 0 0 .26458 9.3567 12.131)" d="m111.22 127.6-56.061-29.92-56.429 29.219 11.132-62.563-45.227-44.638 62.941-8.7459 28.477-56.807 27.768 57.157 62.827 9.5292-45.779 44.071z" style="fill:#20a6ff;paint-order:markers fill stroke"/>
</svg>
```
![](examples/A-2.svg)

here inkscape has assigned the path tag to our more complex image and we can see that extra styling has also been applied

<br>

## apply your own styling css to svg
now that we know the basic of how svgs are set up with can apply our own stylings to these files so take the above example with the star and lets remove the style section from it, for ease of showing i will not include the svg tag from further examples.
 ```
<path transform="matrix(.26458 0 0 .26458 9.3567 12.131)" d="m111.22 127.6-56.061-29.92-56.429 29.219 11.132-62.563-45.227-44.638 62.941-8.7459 28.477-56.807 27.768 57.157 62.827 9.5292-45.779 44.071z"/>
 ```
now lets apply css to this path tag, make a new line below svg tag and above the path tag, open a style tag and lets do apply a simple fill color
 ```
<style>
path {
fill: magenta;
}
</style>
```
so the whole thing become like this

<details>
  <summary>click me to read</summary>
  
<br>

```
<svg width="48.157mm" height="45.893mm" version="1.1" viewBox="0 0 48.157 45.893" xmlns="http://www.w3.org/2000/svg">

<style>
path {
fill: magenta;
}
</style>

<path transform="matrix(.26458 0 0 .26458 9.3567 12.131)" d="m111.22 127.6-56.061-29.92-56.429 29.219 11.132-62.563-45.227-44.638 62.941-8.7459 28.477-56.807 27.768 57.157 62.827 9.5292-45.779 44.071z"/>

</svg>
```
 
</details>

![](examples/B-1.svg)

the color can also be hex `#FF00FF` or `rgb(255, 0, 255)` with the exact same result

<br>

## applying transparency using the color
using hex and rgba colors we can apply transparency (alpha) to these colors as well
 ```
<style>
path {
fill: rgba(255, 0, 255, 0.5);
}
</style>
```

![](examples/B-2.svg)

above example applies 50% opacity to the magenta color, same thing can be achieved by `#FF00FF70`

<br>

## gradients in svg
applying gradient to svg is done by using the gradient tags like `linearGradient` and `radialGradient` tags, here is a simple example for lineargradient for fill color, apply this at the bottom of you style tag and above the actual svg
```
<linearGradient id="grad">
<stop offset="0%" stop-color="cyan" />
<stop offset="100%" stop-color="magenta" />
</linearGradient>
```
you are not limited in setting up these gradients at all and it does not need to start at 0% and end at 100% either, you can have as many colors as you want and at any point yout want, either with transparency (alpha) or not, here is another more involved example
```
<linearGradient id="grad">
<stop offset="20%" stop-color="cyan" />
<stop offset="50%" stop-color="rgba(255, 127, 0, 0.5" />
<stop offset="70%" stop-color="#ff00ff22" />
</linearGradient>
```

as you can see we need to assign an id to this gradient tag and i named mine `grad`, now change your style to include this id and apply the gradint
 ```
<style>
path {
fill: url(#grad);
}
</style>
```
so the whole file becomes like this 
<details>
  <summary>click me to read</summary>
  
<br>

```
<svg width="48.157mm" height="45.893mm" version="1.1" viewBox="0 0 48.157 45.893" xmlns="http://www.w3.org/2000/svg">

<style>
path {
fill: url(#grad);
}
</style>

<linearGradient id="grad">
<stop offset="0%" stop-color="cyan" />
<stop offset="100%" stop-color="magenta" />
</linearGradient>

<path transform="matrix(.26458 0 0 .26458 9.3567 12.131)" d="m111.22 127.6-56.061-29.92-56.429 29.219 11.132-62.563-45.227-44.638 62.941-8.7459 28.477-56.807 27.768 57.157 62.827 9.5292-45.779 44.071z"/>

</svg>
```
</details>

![](examples/C-1.svg)

<br>

## apply animations to your svg
applying animations is easy using css, all you need to do is define a keyframe, assign a name to it and define start and end points to it, lets show a simple example
```
@keyframes test_anim {
0% {
filter: invert(0%);}
100% {
filter: invert(100%);}
}
```
you can also use `from` and `to` instead of `0%` and `100%` if you only need 2 points for your animation but using the percentegas is easier and gives you more control, because these are stylings we apply to these svg files they should also be inside the style tags as your other css

so we made our first animation but why did it not do anything? because you haven't applied it to your path tag yet so lets do that now
```
path {
fill: url(#grad);
animation: test_anim linear 2.5s infinite alternate;
}
```
what happened? so we tell css we want to apply an `animation` to this path tag, we apply the name of our animation `test_anim`, set the style of aniamation we want to use `linear` this can be `ease`, `ease-in-out` and some extra varients, specify the animation length set to `2.5s` seconds in this example and apply this animation `infinite` infinitly and `alternate` makes sure to go back and forth to not have a jarring finish to the animation

here is how it comes together 

<details>
  <summary>click me to read</summary>
<br>
 
```
<svg width="83.166mm" height="79.839mm" version="1.1" viewBox="0 0 83.166 79.839" xmlns="http://www.w3.org/2000/svg">

<style>
@keyframes test_anim {
0% {
filter: invert(0%);}
100% {
filter: invert(100%);}
}

path {
fill: url(#grad);
animation: test_anim linear 2.5s infinite alternate;
}
</style>

<linearGradient id="grad">
<stop offset="0%" stop-color="cyan" />
<stop offset="100%" stop-color="magenta" />
</linearGradient>

<path transform="matrix(.26458 0 0 .26458 9.3567 12.131)" d="m111.22 127.6-56.061-29.92-56.429 29.219 11.132-62.563-45.227-44.638 62.941-8.7459 28.477-56.807 27.768 57.157 62.827 9.5292-45.779 44.071z"/>

</svg>
```
</details>

![](examples/C-2.svg)

<br>

## different filters in css
there are a bunch of filters we can apply in our animations, for a complete explanation on them go this [page](https://developer.mozilla.org/en-US/docs/Web/CSS/filter) but here is simple table to gives you the summery

| filter | minimum | maximum | default | info |
|---|---|---|---|---|
| `blur()` | 0px | n/a | 0px | apply blur effect |
| `brightness()` | 0.0 | 2.0 | 1.0 | assign brightness value |
| `contrast()` | 0% | 200% | 100% | assign contrast value |
| `drop-shadow()` | 0px | n/a | 0px | apply drop shadowing |
| `grayscale()` | 0% | 100% | 0% | apply grayscale (black and white) |
| `hue-rotate()` | 0deg | 360deg | 0deg | rotate hue (change colors) |
| `invert()` | 0% | 100% | 0% | invert colors |
| `opacity()` | 0% | 100% | 100% | change opacity(alpha) |
| `saturate()` | 0% | 200% | 100% | saturate colors |
| `sepia()` | 0% | 100% | 0% | apply sepia (old timey color) |

chaining filters is easy too, just do this:
```
filter: invert(75%) hue-rotate(180deg);
```
