
2025-07-02 20:11

Status:

Tags: [Css Tricks](3%20-%20Tags/Css%20Tricks.md) [CSS](3%20-%20Tags/CSS.md)

---
# How do I make Irregular border in html and Css

[Reddit Question](https://www.reddit.com/r/css/comments/1lov8gv/how_do_i_make_this_border_in_html_and_css/)
### Solution 1
[Codepen Link](https://codepen.io/tomhermans/pen/WbvWWzB)
[Another Codepen Link](https://codepen.io/eclarrrk/pen/VYLNgQR)
[![Comment Image](https://preview.redd.it/how-do-i-make-this-border-in-html-and-css-irregular-border-v0-v5alj2tcl8af1.jpeg?width=1220&format=pjpg&auto=webp&s=c3e9e81bd47314c079ed8140272f6dd6b751030f)](https://preview.redd.it/how-do-i-make-this-border-in-html-and-css-irregular-border-v0-v5alj2tcl8af1.jpeg?width=1220&format=pjpg&auto=webp&s=c3e9e81bd47314c079ed8140272f6dd6b751030f)
Check out SVG filters, E.g.
```jsx
<filter id="wiggle"> <feturbulence basefrequency="0.02" id="turbulence-3" numoctaves="3" result="noise" seed="3"></feturbulence> <fedisplacementmap in2="noise" in="SourceGraphic" scale="3"></fedisplacementmap> </filter>
```

Then apply it with filter: url(#wiggle) to your element.

Play with the values numoctaves, seed, scale etc for different results

Note: the svg should be IN your code. You can hide it by setting it's width and height to zero or other screen-hidden techniques.

```jsx
<svg id="svgfilters" height="0" style="width: 0; height: 0;" viewBox="0 0 1400 1400" xmlns="\\\[\[[[http://www.w3.org/2000/svg\\\](http://www.w3.org/2000/svg)\](http://www.w3.org/2000/svg\](http://www.w3.org/2000/svg))](http://www.w3.org/2000/svg\](http://www.w3.org/2000/svg)](http://www.w3.org/2000/svg](http://www.w3.org/2000/svg)))](http://www.w3.org/2000/svg///]\(http://www.w3.org/2000/svg\)/]\(http://www.w3.org/2000/svg/]\(http://www.w3.org/2000/svg\)\)]\(http://www.w3.org/2000/svg/]\(http://www.w3.org/2000/svg\)]\(http://www.w3.org/2000/svg]\(http://www.w3.org/2000/svg\)\)\))" clip-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2"> <defs> YOUR FILTER OR MULTIPLE FILTERS WITH DIFFERENT ID's </defs> </svg>
```

Edit: error-fix

Edit 2: didn't think about it earlier but, when you apply this filter to a div it also affects everything inside the div. So you might want to resort to putting the border or anything on a pseudo and apply the filter there, leaving the contents unfiltered.

---
### Solution 2

Try with a border-image: [https://developer.mozilla.org/en-US/docs/Web/CSS/border-image](https://developer.mozilla.org/en-US/docs/Web/CSS/border-image)


---
## References