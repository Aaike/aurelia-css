Stylesheets can be loaded by specifying metadata for the VM.

Styles can be added at the document level or as [scoped css](https://github.com/PM5544/scoped-polyfill) or they can be injected into the [shadow dom](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-101).

## @style

This decorator is used to load styles into the document header.
The style is only injected once for multiple instances.

Once all instances have been destroyed the style is removed from the document.

```language-javascript
import {style} from "aurelia-framework";

@style
export class Foo {...}
```

## @scopedStyle

Styles inject with this decorator will be added to the DOM element of the VM.
the `scoped` attribute is set on the style tag to make use of [scoped css](https://github.com/PM5544/scoped-polyfill).

```language-javascript
import {scopedStyle} from "aurelia-framework";

@scopedStyle
export class Foo {...}
```

## @shadowStyle

This decorator should be used with the `@useShadowDOM` decorator.  
It will inject the styles into the shadow root when the view is created.  
note that css injected into a shadow dom is [encapsulated](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/#toc-style-scoped)

```language-javascript
import {shadowStyle} from "aurelia-framework";

@shadowStyle
export class Foo {...}
```

## non conventional use

A parameter can be used with the decorator to specify which css file to load.  
Note that the path is actually a module name that will be resolved using the es6 module loader.

```language-javascript
@style("styles/style.css")
export class Foo {...}
```

Multiple styles can be specified using multiple arguments.

```language-javascript
@style("styles/style.css","styles/anotherStyle.css")
export class Foo {...}
```

## Why 3 separate decorators ?

It is needed for the framework to support all use cases.  
The `@style`, `@scopedStyle` and `@shadowStyle` can be used simultanously to have a VM that will inject css
into the document as well as injecting locally scoped css and also css that is injected into it's shadow dom.
