# REI Code Style Guides // HTML

> Code style guide for HTML at REI

*A mostly reasonable approach to HTML, inspired by [Airbnb's excellent style guide][airbnb-js-styleguide] and [Google's HTML/CSS style guide](google-html-css-style-guide)*

[airbnb-js-styleguide]: //github.com/airbnb/javascript
[google-html-css-style-guide]: //google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml

<a name='TOC'>Table of Contents</a>
-----------------------------------

  1. [General Style Rules](#general)
    * [Protocol](#protocol)
    * [Doctype](#doctype)
    * [Indentation](#indentation)
    * [Capitalization](#capitalization)
    * [Comments](#comments)
    * [Type Attributes](#type-attributes)
  1. [`<head>` Section](#head)
    * [`<meta>` Elements](#meta)
    * [`<link>` Elements](#link)
  1. [Accessibility](#accessibility)
    * [WAI-ARIA](#wai-aria)
  1. [Semantic Markup](#semantics)
    * [HTML5 Semantic Elements](#semantic-elements)
    * [Kraken's H Elements](#h-elements)
  1. [JSP Scriptlets](#scriptlets)
  1. [References](#references)
  1. [Tidbits](#tidbits)
  1. [License](#license)

<a name='general'>General Style Rules</a>
-----------------------------------------

### <a name='protocol'>Protocol</a>

### <a name='doctype'>Doctype</a>

### <a name='indentation'>Indentation</a>

- As with the rest of REI.com, use four-space soft-tabs to indent child elements when it makes sense to put them on a new line.

### <a name='capitalization'>Capitalization</a>

### <a name='comments'>Comments</a>

### <a name='type-attributes'>Type Attributes</a>

<a name='head'>`<head>` Section</a>
-----------------------------------

### <a name='meta'>`<meta>` Elements</a>

### <a name='link'>`<link>` Elements</a>

<a name='accessibility'>Accessibility</a>
-----------------------------------------

### <a name='wai-aria'>WAI-ARIA</a>

<a name='semantics'>Semantic Markup</a>
-----------------------------------------------------

### <a name='semantic-elements'>HTML5 Semantic Elements</a>

- Stick to a consistent hierarchy. If placing one element inside of another requires an explanation, it's probably best not to do it. When in doubt, consult the [MDN](//developer.mozilla.org/en-US/docs/Web/HTML).

- Basic structure for a page:

```html
<html>
<head>
    <title>Title</title>
    <meta charset="utf-8">
    <!-- more meta -->
    <link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
    <header>
        <h1>Header for the page</h1>
        <nav>
            <ul>
                <li><a href="somewhere" title="somewhere">Navigational link for the page</a></li>
            </ul>
        </nav>
    </header>
    <main role="main">
        <article>
            <section>
                <h1>Header for this section</h1>
                <p>Primary content of this section</p>
                <aside>Something related to this section</aside>
            </section>
            <!-- and so on -->
        </article>
    </main>
    <footer>
        <p>Footer-y stuff, like copyright information</p>
    </footer>
</body>
</html>
```

- **Heads-up!** The [`main` element is not yet supported in all browsers](#main-element-compatibility) (although it is poly-filled by HTML5-shiv), so keep that in mind when structuring a page.

### <a name='h-elements'>Kraken's H Elements</a>

### <a name='scriptlets'>JSP Scriptlets</a>

- No.

<a name='references'>References</a>
-----------------------------------

  - [Mozilla Developer Network](mdn)

<a name='tidbits'>Tidbits</a>
-----------------------------

  - <a name='main-element-compatibility'>[`main` element browser compatibility](//developer.mozilla.org/en-US/docs/Web/HTML/Element/main#Browser_compatibility)</a>


## <a name='license'>License</a>

(The MIT License)

Copyright (c) 2013 Recreational Equipment Inc.

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[TOP](#TOC)**

# `</html>`
