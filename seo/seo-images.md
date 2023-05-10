# WEB & IMAGES

## CORE WEB VITALS & SEO

Webp is one of the best formats for the webp.
HTML <img> element should make use of attributes: alt, srcset, sizes and lazy if possible.
Alt attribute must be unique in the page.
Images size should possibly be between 70K & 200K depending on its role inside the page, to decrease image size it might be compressed.
It's a good practice to load different images on different viewports throught srcset attribute.
Might be useful to store images on an external storage (bucket/worker node) to optimize loading times.


## SRCSET & SIZES ATTRIBUTE

Srcset defines the set of images we will allow the browser to choose between, and what size each image is.
Sizes defines a set of media conditions to indicate witch image must be used.
Srcset attribute uses w unit instead px, use the size of OS image inspect tab.

```
<img
  srcset="elva-fairy-480w.jpg 480w, elva-fairy-800w.jpg 800w"
  sizes="(max-width: 600px) 480px,
         800px"
  src="elva-fairy-800w.jpg"
  alt="Elva dressed as a fairy"
/>
```

## PICTURE ELEMENT

The <picture> element is a wrapper containing several <source> elements that provide different sources for the browser to choose from, followed by the all-important <img> element. 

```
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg" />
  <source media="(min-width: 800px)" srcset="elva-800w.jpg" />
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva" />
</picture>
```

## FIGURE & FIGCAPTION ELEMENT

Usually a <figure> element is an image, illustration, diagram, code snippet, etc., that is referenced in the main flow of a document.
It might contain a <figcaption> element to describe the image.

```
<figure>
  <img src="favicon-192x192.png" alt="The beautiful MDN logo." />
  <figcaption>MDN Logo</figcaption>
</figure>
```

```
<figure>
  <figcaption>Get browser details using <code>navigator</code>.</figcaption>
  <pre>
    function NavigatorExample() {
    var txt;
    txt = "Browser CodeName: " + navigator.appCodeName + "; ";
    txt+= "Browser Name: " + navigator.appName + "; ";
    txt+= "Browser Version: " + navigator.appVersion  + "; ";
    txt+= "Cookies Enabled: " + navigator.cookieEnabled  + "; ";
    txt+= "Platform: " + navigator.platform  + "; ";
    txt+= "User-agent header: " + navigator.userAgent  + "; ";
    console.log("NavigatorExample", txt);
    }
  </pre>
</figure>
```

<figcaption> element must be the first or the last child of the <figure> element