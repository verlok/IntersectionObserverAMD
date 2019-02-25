# IntersectionObserverAMD

The [W3C IntersectionObserver Polyfill](https://github.com/w3c/IntersectionObserver), served in AMD.

## Why AMD?

Because with AMD you can load the `IntersectionObserver` **only where it's needed**, as dependency of another script, e.g. [vanilla lazyload](https://github.com/verlok/lazyload).

## How to use

Insert [Require.JS](https://requirejs.org/)'s script (or another AMD module loader) in your page.

```html
<script src="https://cdn.jsdelivr.net/npm/requirejs@2.3.6/bin/r.min.js"></script>
```

In your script, create a dependencies array. 
For example, if you need `IntersectionObserver` polyfill and vanilla-lazyload, do like that:

```js
var dependencies = [
    "IntersectionObserver" in window
        ? null
        : "./vendor/intersection-observer-amd.js",
    "../dist/lazyload.amd.js"
];
```

Finally, use require to execute your script, having the dependecies loaded in the right order and ready to use.

```js
require(dependencies, function(_, LazyLoad) {
    window.ll = new LazyLoad({
        elements_selector: ".lazy",
        // More options?
    });
});
```

[DEMO](https://verlok.github.io/lazyload/demos/amd_polyfill.html) - [SOURCE](https://github.com/verlok/lazyload/blob/master/demos/amd_polyfill.html)

---

To update this in case the guys at W3C improve their polyfill:

```
rollup --format=amd --output=intersection-observer-amd.js -- intersection-observer.js
```