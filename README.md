## svg animations
svgs are the most popular extension for vector images, unlike rastor images (jpg, png ...) vector images dont contain pixels but calculations of the shapes that make the final image

this makes them easier to scale without the quality loss and it usually makes them take smaller file size if you are working with simple shapes

## the basic layout of svg images
svgs are very easy to modify since they are made of calculations, if we open a svg file with a text editor you can see that it's actually really easy to understand

everything is inside tags `<>` with the `svg` tag containing everything, here is the code for a very simple svg image of a rectangle i quickly made in inkscape so we can take a look inside 
```
<svg width="47.404mm" height="21.129mm" version="1.1" viewBox="0 0 47.404 21.129" xmlns="http://www.w3.org/2000/svg">
<rect width="47.404" height="21.129" style="fill:#20a6ff;paint-order:markers fill stroke"/>
</svg>
```
![](step1/A-1.svg)

the svg tag contains the width and height of our image, note that this is the value you decided in your svg editor and can be easily changed, the reason for these to exist is so we can have a default value.

the rect tag here contains x coordinantes, width and height and some styling we applied in our svg editor (in my case inkscape)

note that this rect tag was created because i made a very simple rectangle image, if we make a more complex shape this tag changes depending the complexity, here is another example:
```
<svg width="48.157mm" height="45.893mm" version="1.1" viewBox="0 0 48.157 45.893" xmlns="http://www.w3.org/2000/svg">
<path transform="matrix(.26458 0 0 .26458 9.3567 12.131)" d="m111.22 127.6-56.061-29.92-56.429 29.219 11.132-62.563-45.227-44.638 62.941-8.7459 28.477-56.807 27.768 57.157 62.827 9.5292-45.779 44.071z" style="fill:#20a6ff;paint-order:markers fill stroke"/>
</svg>
```
![](step1/A-2.svg)

here inkscape has assigned the path tag to our more complex image and we can see that extra styling has also been applied

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

![](step2/B-1.svg)

the color can also be hex `#FF00FF` or `rgb(255, 0, 255)` with the exact same result

## applying transparency using the color
using hex and rgba colors we can apply transparency (alpha) to these colors as well
 ```
<style>
path {
fill: rgba(255, 0, 255, 0.5);
}
</style>
```

![](step2/B-2.svg)

above example applies 50% opacity to the magenta color, same thing can be achieved by `#FF00FF70`

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
![](step3/C-1.svg)