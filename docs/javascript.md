# [REI Code Style Guides](/README.md) // JavaScript

> Code style guide for JavaScript at REI

A mostly reasonable approach to JavaScript, forked and modified from [Airbnb's excellent JavaScript style guide][airbnb-js-styleguide](//github.com/airbnb/javascript).

Here's a quick example of JavaScript formatted following this code style guide:

```js
'use strict';

function foo ( fizz, buzz, firstName ) {
    bar( 1, buzz );

    var lastName;
    var idx     = 0;
    var myObj   = { 0: 'zero', 1: 'one' };
    var myArray = [ 0, 1, 2 ];

    if ( firstName === 'Homer' ) {
        lastName = 'Simpson';
    }

    if ( !idx > 10 ) {
        for ( var deeperIdx = 0; deeperIdx < 10; deeperIdx++ ) {
            switch ( deeperIdx ) {
                case 0:
                    value = 'zero';
                    break;
                case 1:
                    value = 'one';
                    break;
            }
            var result = deeperIdx > 5 ? 'GT 5' : 'LE 5';
        }
    } else {
        var evenDeeperIdx = 0;
        try {
            while ( evenDeeperIdx < 10 ) {
                if ( idx === evenDeeperIdx || evenDeeperIdx > 5 ) {
                    myArray[ evenDeeperIdx ] = idx + evenDeeperIdx * 12;
                }
                idx = ( evenDeeperIdx << 2 ) & 4;
                evenDeeperIdx++;
            }
            do {
                evenDeeperIdx--;
            } while ( evenDeeperIdx > 0 )
        } catch ( err ) {
            alert( 'Failure: ' + err.message );
        } finally {
            reset( myArray, idx );
        }
    }
}

```

<a name='TOC'>Table of Contents</a>
-----------------------------------

1. [Inspiration, or: Why?](#inspiration)
1. [Types](#types)
1. [Objects](#objects)
1. [Arrays](#arrays)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Properties](#properties)
1. [Variables](#variables)
1. [Hoisting](#hoisting)
1. [Conditional Expressions & Equality](#conditionals)
1. [Blocks](#blocks)
1. [Comments](#comments)
1. [Whitespace](#whitespace)
1. [Commas](#commas)
1. [Semicolons](#semicolons)
1. [Type Casting & Coercion](#type-coercion)
1. [Naming Conventions](#naming-conventions)
1. [Accessors](#accessors)
1. [Constructors](#constructors)
1. [Events](#events)
1. [Modules](#modules)
1. [jQuery](#jquery)
1. [ES5 Compatibility](#es5)
1. [Performance](#performance)
1. [Resources](#resources)
1. [In the Wild](#in-the-wild)
1. [Translation](#translation)
1. [Contributors](#contributors)
1. [License](#license)


<a name='inspiration'>Inspiration</a>
-------------------------------------

From [PEP-20: The Zen of Python](//www.python.org/dev/peps/pep-0020/):

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!


From [Steve Kwan](#kwan-best-practices):

> I don't write my code to impress the parser. I write it for the people after me who will have to understand it.

<a name='types'>Types</a>
-------------------------

- **Primitives:** When you access a primitive type you work directly on its value.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = 1;
    var bar = foo;

    bar = 9;

    console.log( foo, bar ); // => 1, 9
    ```

- **Complex:** When you access a complex type you work on a reference to its value.

    + `object`
    + `array`
    + `function`

    ```javascript
    var foo = [ 1, 2 ];
    var bar = foo;

    bar[ 0 ] = 9;

    console.log( foo[ 0 ], bar[ 0 ] ); // => 9, 9
    ```

[[↑ back to top]](#TOC)


<a name='objects'>Objects</a>
-----------------------------

- Use the literal syntax for object creation.

    ```javascript
    // good
    var item = {};

    // bad
    var item = new Object();
    ```

- Don't use [reserved words](//es5.github.io/#x7.6.1) as keys. It won't work in IE8. ([More info](//github.com/airbnb/javascript/issues/61))

    ```javascript
    // good
    var superman = {
        defaults: { clark: 'kent' },
        hidden: true
    };

    // bad
    var superman = {
        default: { clark: 'kent' },
        private: true
    };
    ```

- Use readable synonyms in place of reserved words.

    ```javascript
    // good
    var superman = {
        type: 'alien'
    };

    // bad
    var superman = {
        class: 'alien'
    };

    // bad
    var superman = {
        klass: 'alien'
    };
    ```

[[↑ back to top]](#TOC)


<a name='arrays'>Arrays</a>
---------------------------

- Use the literal syntax for array creation.

    ```javascript
    // good
    var items = [];

    // bad
    var items = new Array();
    ```

- If you don't know array length use Array#push.

    ```javascript
    var someStack = [];

    // good
    someStack.push( 'abracadabra' );

    // bad
    someStack[ someStack.length ] = 'abracadabra';
    ```

- When you need to copy an array use Array#slice. ([jsPerf](//jsperf.com/converting-arguments-to-an-array/7))

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // good
    itemsCopy = items.slice();

    // bad
    for ( i = 0; i < len; i++ ) {
        itemsCopy[ i ] = items[ i ];
    }
    ```

- To convert an array-like object to an array, use Array#slice.

    ```javascript
    function trigger () {
        var args = Array.prototype.slice.call( arguments );
        ...
    }
    ```

[[↑ back to top]](#TOC)


<a name='strings'>Strings</a>
-----------------------------

- Use single quotes (`''`) for strings.

    ```javascript
    // good
    var name = 'Bob Parr';

    // bad
    var name = "Bob Parr";

    // good
    var fullName = 'Bob ' + this.lastName;

    // bad
    var fullName = "Bob " + this.lastName;
    ```

- Strings longer than 80 characters should be written across multiple lines
  using string concatenation. (**Note:** If overused, long strings with
  concatenation could impact performance. See this
  [jsperf](//jsperf.com/ya-string-concat) and
  [discussion](//github.com/airbnb/javascript/issues/40).)

    ```javascript
    // good
    var errorMessage = 'This is a super long error that ' +
        'was thrown because of Batman.' +
        'When you stop to think about ' +
        'how Batman had anything to do ' +
        'with this, you would get nowhere ' +
        'fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that \
    was thrown because of Batman. \
    When you stop to think about \
    how Batman had anything to do \
    with this, you would get nowhere \
    fast.';
    ```

- When programatically building up a string, use Array#join instead of string
  concatenation. Mostly for IE: [jsPerf](//jsperf.com/string-vs-array-concat/2).

    ```javascript
    var items;
    var messages;
    var length;
    var i;

    messages = [{
        state: 'success',
        message: 'This one worked.'
    },{
        state: 'success',
        message: 'This one worked as well.'
    },{
        state: 'error',
        message: 'This one did not work.'
    }];

    length = messages.length;

    // good
    function inbox ( messages ) {
        items = [];

        for ( i = 0; i < length; i++ ) {
          items[ i ] = messages[ i ].message;
        }

        return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
    }

    // bad
    function inbox ( messages ) {
        items = '<ul>';

        for ( i = 0; i < length; i++ ) {
            items += '<li>' + messages[i].message + '</li>';
        }

        return items + '</ul>';
    }
    ```
- As much as possible, strings should be externalized to a separate "strings" module. This makes our code more readable, DRYer, and easier to maintain. Examples where this makes sense: data attribute names, selectors, events, etc.

    ```javascript
    // strings.js
    module.exports.selectors = {
        item:  '.item',
        items: '.items'
    };

    module.exports.events = {
        thingUpdated: 'updated.thing',
        thingClosed:  'closed.thing'
    };
    ```

    ```javascript
    // example-usage.js
    var strings   = require( './strings' );
    var selectors = strings.selectors;
    var events    = strings.events;

    $( document ).bind( events.thingUpdated, function () {
        // do things
    });

    $( document ).delegate( selectors.items, 'click', function () {
        // do stuff
    });
    ```

[[↑ back to top]](#TOC)


<a name='functions'>Functions</a>
---------------------------------

- [Function expressions](#nfe-demystified):

    ```javascript
    // anonymous function expression
    var anonymous = function () {
        return true;
    };

    // named function expression
    var named = function named () {
        return true;
    };

    // immediately-invoked function expression (IIFE)
    (function () {
        console.log( 'Welcome to the Internet. Please follow me.' );
    })();
    ```

- Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears. (**Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262's note on this issue](//www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).)

    ```javascript
    // good
    var test;
    if ( currentUser ) {
        test = function test () {
            console.log( 'Yup.' );
        };
    }

    // bad
    if ( currentUser ) {
        function test () {
            console.log( 'Nope.' );
        }
    }
    ```

- Never name a parameter `arguments`, this will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // good
    function yup ( name, options, args ) {
        // ...stuff...
    }

    // bad
    function nope ( name, options, arguments ) {
        // ...stuff...
    }
    ```

- Avoid recursion. Use iteration instead. JavaScript does not ([yet](http://bbenvie.com/articles/2013-01-06/JavaScript-ES6-Has-Tail-Call-Optimization)) have proper tail-calls, so every call adds a frame to the stack.

    ```javascript
    // better
    function fact ( n ) {
        var total = 1;
        while ( n ) {
            total = total * n;
            --n;
        }
        return total;
    }
    fact( 40000 ); // => Infinity (in Chrome; not correct, but that's because of JavaScript's MaxInt)

    // bad
    function fact ( n, total ) {
        return n > 0 ? fact( n - 1, n * total ) : 1;
    }
    fact( 40000, 1 ); // => RangeError: Maximum call stack size exceeded (in Chrome)
    ```

[[↑ back to top]](#TOC)


<a name='properties'>Properties</a>
-----------------------------------

- Use dot notation when accessing properties.

    ```javascript
    var luke = {
        jedi: true,
        age: 28
    };

    // good
    var isJedi = luke.jedi;

    // bad
    var isJedi = luke[ 'jedi' ];
    ```

- Use subscript notation (`[]`) when accessing properties with a variable.

    ```javascript
    var luke = {
        jedi: true,
        age: 28
    };

    function getProp ( prop ) {
        return luke[ prop ];
    }

    var isJedi = getProp( 'jedi' );
    ```

[[↑ back to top]](#TOC)


<a name='variables'>Variables</a>
---------------------------------

- Always use `var` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.

    ```javascript
    // good
    var superPower = new SuperPower();

    // bad
    superPower = new SuperPower();
    ```

- Use one `var` declaration per variable and declare each variable on a newline.

    ```javascript
    // good
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';

    // bad
    var items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';
    ```

- Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    // good
    var items = getItems();
    var goSportsTeam = true;
    var dragonball;
    var length;
    var i;

    // bad
    var i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // still bad
    var i;
    var items = getItems();
    var dragonball;
    var goSportsTeam = true;
    var len;
    ```

- Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

    ```javascript
    // good
    function () {
        var name = getName();

        test();
        console.log( 'doing stuff..' );

        //..other stuff..

        if ( name === 'test' ) {
            return false;
        }

        return name;
    }

    // bad
    function () {
        test();
        console.log( 'doing stuff..' );

        //..other stuff..

        var name = getName();

        if ( name === 'test' ) {
            return false;
        }

        return name;
    }

    // good
    function () {
        if ( !arguments.length ) {
            return false;
        }

        var name = getName();

        return true;
    }

    // bad
    function () {
        var name = getName();

        if ( !arguments.length ) {
            return false;
        }

        return true;
    }
    ```

[[↑ back to top]](#TOC)


<a name='hoisting'>Hoisting</a>
-------------------------------

- Variable declarations get hoisted to the top of their scope, their assignment does not.

    ```javascript
    // we know this wouldn't work (assuming there
    // is no notDefined global variable)
    function example () {
        console.log( notDefined ); // => throws a ReferenceError
    }

    // creating a variable declaration after you
    // reference the variable will work due to
    // variable hoisting. Note: the assignment
    // value of `true` is not hoisted.
    function example () {
        console.log( declaredButNotAssigned ); // => undefined
        var declaredButNotAssigned = true;
    }

    // The interpreter is hoisting the variable
    // declaration to the top of the scope.
    // Which means our example could be rewritten as:
    function example () {
        var declaredButNotAssigned;
        console.log( declaredButNotAssigned ); // => undefined
        declaredButNotAssigned = true;
    }
    ```

- Anonymous function expressions hoist their variable name, but not the function assignment.

    ```javascript
    function example () {
        console.log( anonymous ); // => undefined

        anonymous(); // => TypeError anonymous is not a function

        var anonymous = function () {
            console.log( 'anonymous function expression' );
        };
    }
    ```

- Named function expressions hoist the variable name, not the function name or the function body.

    ```javascript
    function example () {
        console.log( named ); // => undefined

        named(); // => TypeError named is not a function

        superPower(); // => ReferenceError superPower is not defined

        var named = function superPower () {
            console.log( 'Flying' );
        };
    }

    // the same is true when the function name
    // is the same as the variable name.
    function example () {
        console.log( named ); // => undefined

        named(); // => TypeError named is not a function

        var named = function named () {
            console.log( 'named' );
        }
    }
    ```

- Function declarations hoist their name and the function body.

    ```javascript
    function example () {
        superPower(); // => Flying

        function superPower () {
            console.log( 'Flying' );
        }
    }
    ```

For more information refer to [JavaScript Scoping & Hoisting](//www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](//www.adequatelygood.com/).

[[↑ back to top]](#TOC)


<a name='conditionals'>Conditional Expressions & Equality</a>
-------------------------------------------------------------

- Use `===` and `!==` over `==` and `!=`.

- Conditional expressions are evaluated using coercion with the `ToBoolean` method and always follow these simple rules:

    + **Objects** evaluate to **true**
    + **Undefined** evaluates to **false**
    + **Null** evaluates to **false**
    + **Booleans** evaluate to **the value of the boolean**
    + **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ( [ 0 ] ) {
        // true
        // An array is an object, objects evaluate to true
    }
    ```

- Use shortcuts.

    ```javascript
    // good
    if ( name ) {
        // ...stuff...
    }

    // bad
    if ( name !== '' ) {
        // ...stuff...
    }

    // good
    if ( collection.length ) {
        // ...stuff...
    }

    // bad
    if ( collection.length > 0 ) {
        // ...stuff...
    }
    ```

For more information see [Truth Equality and JavaScript](//javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

[[↑ back to top]](#TOC)


<a name='blocks'>Blocks</a>
---------------------------

- Use braces with all multi-line blocks.

    ```javascript
    // good
    if ( test ) return false;

    // good
    if ( test ) {
        return false;
    }

    // good
    function () {
        return false;
    }

    // bad
    if ( test )
        return false;

    // bad
    function () { return false; }
    ```

[[↑ back to top]](#TOC)


<a name='comments'>Comments</a>
-------------------------------

- Use `/** ... */` for multiline comments. Include a description, specify types and values for all parameters and return values.

    ```javascript
    // good
    /** make () returns a new element
        based on the passed in tag name

        @param <String> tag
        @return <Element> element
     */
    function make ( tag ) {

        // ...stuff...

        return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param <String> tag
     * @return <Element> element
     */
    function make ( tag ) {

        // ...stuff...

        return element;
    }

    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param <String> tag
    // @return <Element> element
    function make ( tag ) {

        // ...stuff...

        return element;
    }
    ```

- Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment.

    ```javascript
    // good
    // is current tab
    var active = true;

    // good
    function getType () {
        console.log( 'fetching type...' );

        // set the default type to 'no type'
        var type = this._type || 'no type';

        return type;
    }

    // bad
    var active = true;  // is current tab

    // bad
    function getType () {
        console.log( 'fetching type...' );
        // set the default type to 'no type'
        var type = this._type || 'no type';

        return type;
    }
    ```

- Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME -- need to figure this out` or `TODO -- need to implement`.

- Use `// FIXME:` to annotate problems

    ```javascript
    function Calculator () {

        // FIXME: shouldn't use a global here
        total = 0;

        return this;
    }
    ```

- Use `// TODO:` to annotate solutions to problems

    ```javascript
    function Calculator () {

        // TODO: total should be configurable by an options param
        this.total = 0;

        return this;
    }
    ```

[[↑ back to top]](#TOC)


<a name='whitespace'>Whitespace</a>
-----------------------------------

- Use soft tabs (tabs composed of spaces) set to 4 spaces

    ```javascript
    // good
    function () {
    ∙∙∙∙var name;
    }

    // bad
    function () {
    ∙∙∙var name;
    }

    // bad
    function () {
    ∙∙var name;
    }

    // bad
    function () {
    ∙var name;
    }

    ```

- Place 1 space before the leading brace.

    ```javascript
    // good
    function test () {
        console.log( 'test' );
    }

    // good
    dog.set( 'attr', {
        age:    '1 year',
        breed:  'Bernese Mountain Dog'
    } );

    // bad
    function test (){
        console.log( 'test' );
    }

    // bad
    dog.set( 'attr',{
        age:    '1 year',
        breed:  'Bernese Mountain Dog'
    } );

    ```

- **Breathing Room:** Place 1 space inside and outside parens of expressions, and 1 space inside of calls and subs.

    ```javascript
    // good
    for ( var i = 0; i < foo.length; ++i ) {
        ...
    }

    var f = function ( a, b, c ) {
        ...
    };

    f( 1, 2, 3 );

    a[ 0 ];

    // bad
    for(var i = 0; i < foo.length; ++i) {
        ...
    }

    var f = function(a, b, c) {
        ...
    };

    f(1, 2, 3);

    a[0];
    ```

- Place an empty newline at the end of the file.

    ```javascript
    // good
    ( function ( global ) {
        // ...stuff...
    } )( this );

    ```

    ```javascript
    // bad
    ( function ( global ) {
        // ...stuff...
    } )( this );
    ```

- Use indentation when making long method chains.

    ```javascript
    // good
    $( '#items' )
        .find( '.selected' )
            .highlight()
            .end()
        .find( '.open' )
            .updateCount();

    // bad
    $( '#items' ).find( '.selected' ).highlight().end().find( '.open' ).updateCount();

    // good
    var leds = stage.selectAll( '.led' )
            .data( data )
        .enter().append( 'svg:svg' )
            .class( 'led', true)
            .attr( 'width',  ( r adius + margin ) * 2 )
        .append( 'svg:g' )
            .attr( 'transform', 'translate(' + ( radius + margin ) + ',' + ( radius + margin ) + ')' )
            .call( tron.led );

    // bad
    var leds = stage.selectAll( '.led' ).data( data ).enter().append( 'svg:svg' ).class( 'led', true )
        .attr('width',  (radius + margin) * 2).append('svg:g')
        .attr( 'transform', 'translate(' + ( radius + margin ) + ',' + ( radius + margin ) + ')' )
        .call( tron.led );
    ```

[[↑ back to top]](#TOC)


<a name='commas'>Commas</a>
---------------------------

- Leading commas: **Nope.**

    ```javascript
    // good
    var hero = {
        firstName:  'Bob',
        lastName:   'Parr',
        heroName:   'Mr. Incredible',
        superPower: 'strength'
    };

    // bad
    var hero = {
        firstName: 'Bob'
        , lastName: 'Parr'
        , heroName: 'Mr. Incredible'
        , superPower: 'strength'
    };
    ```

- Additional trailing comma: **Nope.** This can cause problems with IE6/7 and IE9 if it's in quirksmode. Also, in some implementations of ES3 would add length to an array if it had an additional trailing comma. This was clarified in ES5 ([source](//es5.github.io/#D)):

> Edition 5 clarifies the fact that a trailing comma at the end of an ArrayInitialiser does not add to the length of the array. This is not a semantic change from Edition 3 but some implementations may have previously misinterpreted this.

    ```javascript
    // good
    var hero = {
        firstName: 'Kevin',
        lastName: 'Flynn'
    };

    var heroes = [
        'Batman',
        'Superman'
    ];

    // bad
    var hero = {
        firstName: 'Kevin',
        lastName: 'Flynn',
    };

    var heroes = [
        'Batman',
        'Superman',
    ];
    ```

[[↑ back to top]](#TOC)


<a name='semicolons'>Semicolons</a>
-----------------------------------

- **Yup.**

    ```javascript
    // good
    ;( function () {
        var name = 'Skywalker';
        return name;
    } )();

    // good
    ( function () {
        var name = 'Skywalker';
        return name;
    } )();

    // bad
    ( function () {
        var name = 'Skywalker'
        return name
    } )()
    ```

[[↑ back to top]](#TOC)


<a name='type-coercion'>Type Casting & Coersion</a>
---------------------------------------------------

- Perform type coercion at the beginning of the statement.

- Strings:

    ```javascript
    //  => this.reviewScore = 9;

    // good
    var totalScore = '' + this.reviewScore;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = this.reviewScore + ' total score';

    // bad
    var totalScore = '' + this.reviewScore + ' total score';
    ```

- Use `parseInt` for Numbers and always with a radix for type casting.

    ```javascript
    var inputValue = '4';

    // good
    var val = parseInt( inputValue, 10 );

    // acceptable
    var val = Number( inputValue );

    // bad
    var val = new Number( inputValue );

    // bad
    var val = +inputValue;

    // bad
    var val = inputValue >> 0;

    // bad
    var val = parseInt( inputValue );
    ```

- If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](//jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you're doing. (**Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](//es5.github.io/#x4.3.19), but Bitshift operations always return a 32-bit integer ([source](//es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](//github.com/airbnb/javascript/issues/109))

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    var val = inputValue >> 0;
    ```

- Booleans:

    ```javascript
    var age = 0;

    // good
    var hasAge = !!age;

    // good
    var hasAge = Boolean( age );

    // bad
    var hasAge = new Boolean( age );
    ```

[[↑ back to top]](#TOC)


<a name='naming-conventions'>Naming Conventions</a>
---------------------------------------------------

- Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // good
    function query () {
        // ..stuff..
    }

    // bad
    function q () {
        // ...stuff...
    }
    ```

- Use camelCase when naming objects, functions, and instances

    ```javascript
    // good
    var thisIsMyObject = {};
    function thisIsMyFunction () {};
    var user = new User( {
        name: 'Bob Parr'
    } );

    // bad
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    function c() {};
    var u = new user( {
        name: 'Bob Parr'
    } );
    ```

- Use PascalCase when naming constructors or classes

    ```javascript
    // good
    function User ( options ) {
        this.name = options.name;
    }

    var good = new User( {
        name: 'yup'
    } );

    // bad
    function user ( options ) {
        this.name = options.name;
    }

    var bad = new user( {
        name: 'nope'
    } );
    ```

- Use a leading underscore `_` when naming private properties

    ```javascript
    // good
    this._firstName = 'Panda';

    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    ```

- When saving a reference to `this` use `_this` or `self`.

    ```javascript
    // good
    function () {
        var _this = this;
        return function () {
            console.log( _this );
        };
    }

    // good
    function () {
        var self = this;
        return function () {
            console.log( self );
        };
    }

    // bad
    function () {
        var that = this;
        return function () {
            console.log( that );
        };
    }
    ```

- Name your functions. This is helpful for stack traces.

    ```javascript
    // good
    var log = function log ( msg ) {
        console.log( msg );
    };

    // bad
    var log = function ( msg ) {
        console.log( msg );
    };
    ```

[[↑ back to top]](#TOC)


<a name='accessors'>Accessors</a>
---------------------------------

- Accessor functions for properties are not required
- If you do make accessor functions use getVal() and setVal('hello')

    ```javascript
    // good
    dragon.getAge();

    // bad
    dragon.age();

    // good
    dragon.setAge( 25 );

    // bad
    dragon.age( 25 );
    ```

- If the property is a boolean, use isVal() or hasVal()

    ```javascript
    // good
    if ( !dragon.hasAge() ) {
        return false;
    }

    // bad
    if ( !dragon.age() ) {
        return false;
    }
    ```

- It's okay to create get() and set() functions, but be consistent.

    ```javascript
    function Jedi ( options ) {
        options || ( options = {} );
        var lightsaber = options.lightsaber || 'blue';
        this.set( 'lightsaber', lightsaber );
    }

    Jedi.prototype.set = function ( key, val ) {
        this[ key ] = val;
    };

    Jedi.prototype.get = function ( key ) {
        return this[ key ];
    };
    ```

[[↑ back to top]](#TOC)


<a name='constructors'>Constructors</a>
---------------------------------------

- Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

    ```javascript
    function Jedi () {
        console.log( 'new jedi' );
    }

    // good
    Jedi.prototype.fight = function fight () {
        console.log( 'fighting' );
    };

    Jedi.prototype.block = function block () {
        console.log( 'blocking' );
    };

    // bad
    Jedi.prototype = {
        fight: function fight () {
            console.log( 'fighting' );
        },

        block: function block () {
            console.log( 'blocking' );
        }
    };
    ```

- Methods can return `this` to help with method chaining.

    ```javascript
    // good
    Jedi.prototype.jump = function () {
        this.jumping = true;
        return this;
    };

    Jedi.prototype.setHeight = function ( height ) {
        this.height = height;
        return this;
    };

    var luke = new Jedi();

    luke.jump()
        .setHeight( 20 );

    // bad
    Jedi.prototype.jump = function () {
        this.jumping = true;
        return true;
    };

    Jedi.prototype.setHeight = function ( height ) {
        this.height = height;
    };

    var luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight( 20 ) // => undefined
    ```


- It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

    ```javascript
    function Jedi ( options ) {
        options || ( options = {} );
        this.name = options.name || 'no name';
    }

    Jedi.prototype.getName = function getName () {
        return this.name;
    };

    Jedi.prototype.toString = function toString () {
        return 'Jedi - ' + this.getName();
    };
    ```

[[↑ back to top]](#TOC)


<a name='events'>Events</a>
---------------------------

- When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```js
    // good
    $(this).trigger( 'listingUpdated', {
        listingId: listing.id
    });

    ...

    $(this).on( 'listingUpdated', function ( e, data ) {
        // do something with data.listingId
    });


    // bad
    $(this).trigger( 'listingUpdated', listing.id );

    ...

    $(this).on( 'listingUpdated', function ( e, listingId ) {
        // do something with listingId
    });
    ```

[[↑ back to top]](#TOC)


<a name='modules'>Modules</a>
-----------------------------

- The module should start with a `!`. This ensures that if a malformed module forgets to include a final semicolon there aren't errors in production when the scripts get concatenated. [Explanation](//github.com/airbnb/javascript/issues/44#issuecomment-13063933)
- The file should be named with camelCase, live in a folder with the same name, and match the name of the single export.
- Add a method called noConflict() that sets the exported module to the previous version and returns this one.
- Always declare `'use strict';` at the top of the module.

    ```javascript
    // fancyInput/fancyInput.js

    !function ( global ) {
        'use strict';

        var previousFancyInput = global.FancyInput;

        function FancyInput ( options ) {
            this.options = options || {};
        }

        FancyInput.noConflict = function noConflict () {
            global.FancyInput = previousFancyInput;
            return FancyInput;
        };

        global.FancyInput = FancyInput;
    }( this );
    ```

[[↑ back to top]](#TOC)


<a name='jquery'>jQuery</a>
---------------------------

- Prefix jQuery object variables with a `$`.

    ```javascript
    // good
    var $sidebar = $( '.sidebar' );

    // bad
    var sidebar = $( '.sidebar' );
    ```

- Cache jQuery lookups.

    ```javascript
    // good
    function setSidebar () {
        var $sidebar = $('.sidebar');
        $sidebar.hide();

        // ...stuff...

        $sidebar.css( {
            'background-color': 'pink'
        } );
    }

    // bad
    function setSidebar () {
        $( '.sidebar' ).hide();

        // ...stuff...

        $( '.sidebar' ).css( {
            'background-color': 'pink'
        } );
    }
    ```

- For DOM queries use Cascading `$( '.sidebar ul' )` or parent > child `$( '.sidebar > ul' )`. [jsPerf](//jsperf.com/jquery-find-vs-context-sel/16)
- Use `find` with scoped jQuery object queries.

    ```javascript
    // good
    $( '.sidebar ul' ).hide();

    // good
    $( '.sidebar > ul' ).hide();

    // good
    $sidebar.find( 'ul' );

    // bad
    $( 'ul', '.sidebar' ).hide();

    // bad
    $( '.sidebar' ).find( 'ul' ).hide();
    ```

[[↑ back to top]](#TOC)


<a name='es5'>ECMAScript 5 Compatibility</a>
--------------------------------------------

    - Refer to [Kangax](//twitter.com/kangax/)'s ES5 [compatibility table](//kangax.github.com/es5-compat-table/)

[[↑ back to top]](#TOC)


<a name='performance'>Performance</a>
-------------------------------------

- [On Layout & Web Performance](//kellegous.com/j/2013/01/26/layout-performance/)
- [String vs Array Concat](//jsperf.com/string-vs-array-concat/2)
- [Try/Catch Cost In a Loop](//jsperf.com/try-catch-in-loop-cost)
- [Bang Function](//jsperf.com/bang-function)
- [jQuery Find vs Context, Selector](//jsperf.com/jquery-find-vs-context-sel/13)
- [innerHTML vs textContent for script text](//jsperf.com/innerhtml-vs-textcontent-for-script-text)
- [Long String Concatenation](//jsperf.com/ya-string-concat)
- [Array construction](//jsperf.com/sized-array-creation)
- Loading...

[[↑ back to top]](#TOC)


<a name='resources'>Resources</a>
---------------------------------

**Read This**

- [Annotated ECMAScript 5.1](//es5.github.com/)

**Other Styleguides**

- [Google JavaScript Style Guide](//google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
- [jQuery Core Style Guidelines](//docs.jquery.com/JQuery_Core_Style_Guidelines)
- [Principles of Writing Consistent, Idiomatic JavaScript](//github.com/rwldrn/idiomatic.js/)
- [PEP 8 - Style Guide for Python](//www.python.org/dev/peps/pep-0008/)

**Other Styles**

- [Naming this in nested functions](//gist.github.com/4135065) - Christian Johansen
- [Conditional Callbacks](//github.com/airbnb/javascript/issues/52)
- [Popular JavaScript Coding Conventions on Github](//sideeffect.kr/popularconvention/#javascript)

**Further Reading**

- [Understanding JavaScript Closures](http://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
- [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
- <a name='nfe-demystified'>[Named function expressions demystified](http://kangax.github.io/nfe/)</a> - Jurly "kangax" Zaytsev
- <a name='kwan-best-practices'>[Steve Kwan's JavaScript Best Practices](//github.com/stevekwan/best-practices/blob/master/javascript/best-practices.md) - Steve Kwan

**Books**

- [JavaScript: The Good Parts](//www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
- [JavaScript Patterns](//www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
- [Pro JavaScript Design Patterns](//www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
- [High Performance Web Sites: Essential Knowledge for Front-End Engineers](//www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
- [Maintainable JavaScript](//www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
- [JavaScript Web Applications](//www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
- [Pro JavaScript Techniques](//www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
- [Smashing Node.js: JavaScript Everywhere](//www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
- [Secrets of the JavaScript Ninja](//www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
- [Human JavaScript](//humanjavascript.com/) - Henrik Joreteg
- [Superhero.js](//superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
- [JSBooks](//jsbooks.revolunet.com/)
- [Refactoring Improving the Design of Existing Code](http://www.amazon.com/Refactoring-Improving-Design-Existing-Code/dp/0201485672/) - Martin Fowler   Note: not JS, but great practices
- [JavaScript Design Patterns](http://addyosmani.com/resources/essentialjsdesignpatterns/book/) - Addy Osmani

**Blogs**

- [DailyJS](//dailyjs.com/)
- [JavaScript Weekly](//javascriptweekly.com/)
- [Bocoup Weblog](//weblog.bocoup.com/)
- [NCZOnline](//www.nczonline.net/)
- [Perfection Kills](//perfectionkills.com/)
- [Ben Alman](//benalman.com/)
- [nettuts](//net.tutsplus.com/?s=javascript)

[[↑ back to top]](#TOC)


<a name='in-the-wild'>In the Wild</a>
-------------------------------------

This is a list of organizations that are using the [original airbnb JavaScript style guide][airbnb-styleguide]:

- **Aan Zee**: [AanZee/javascript](//github.com/AanZee/javascript)
- **Airbnb**: [airbnb/javascript](//github.com/airbnb/javascript)
- **American Insitutes for Research**: [AIRAST/javascript](//github.com/AIRAST/javascript)
- **Compass Learning**: [compasslearning/javascript-style-guide](//github.com/compasslearning/javascript-style-guide)
- **ExactTarget**: [ExactTarget/javascript](//github.com/ExactTarget/javascript)
- **Gawker Media**: [gawkermedia/javascript](//github.com/gawkermedia/javascript)
- **GeneralElectric**: [GeneralElectric/javascript](//github.com/GeneralElectric/javascript)
- **GoodData**: [gooddata/gdc-js-style](//github.com/gooddata/gdc-js-style)
- **Grooveshark**: [grooveshark/javascript](//github.com/grooveshark/javascript)
- **How About We**: [howaboutwe/javascript](//github.com/howaboutwe/javascript)
- **Mighty Spring**: [mightyspring/javascript](//github.com/mightyspring/javascript)
- **MinnPost**: [MinnPost/javascript](//github.com/MinnPost/javascript)
- **ModCloth**: [modcloth/javascript](//github.com/modcloth/javascript)
- **National Geographic**: [natgeo/javascript](//github.com/natgeo/javascript)
- **National Park Service**: [nationalparkservice/javascript](//github.com/nationalparkservice/javascript)
- **Razorfish**: [razorfish/javascript-style-guide](//github.com/razorfish/javascript-style-guide)
- **REI**: [reidev/javascript](//github.com/reidev/javascript)
- **Shutterfly**: [shutterfly/javascript](//github.com/shutterfly/javascript)
- **Userify**: [userify/javascript](//github.com/userify/javascript)
- **Zillow**: [zillow/javascript](//github.com/zillow/javascript)
- **ZocDoc**: [ZocDoc/javascript](//github.com/ZocDoc/javascript)

If you use this fork of the style guide, send us a pull request, and we'll start a list.


<a name='translation'>Translation</a>
-------------------------------------

Translations of the [original airbnb JavaScript style guide][airbnb-styleguide] are available in the following languages:

- :de: **German**: [timofurrer/javascript-style-guide](//github.com/timofurrer/javascript-style-guide)
- :jp: **Japanese**: [mitsuruog/javacript-style-guide](//github.com/mitsuruog/javacript-style-guide)
- :br: **Portuguese**: [armoucar/javascript-style-guide](//github.com/armoucar/javascript-style-guide)
- :cn: **Chinese**: [adamlu/javascript-style-guide](//github.com/adamlu/javascript-style-guide)
- :es: **Spanish**: [paolocarrasco/javascript-style-guide](//github.com/paolocarrasco/javascript-style-guide)
- :kr: **Korean**: [tipjs/javascript-style-guide](//github.com/tipjs/javascript-style-guide)
- :fr: **French**: [nmussy/javascript-style-guide](//github.com/nmussy/javascript-style-guide)
- :ru: **Russian**: [sbezludny/javascript-style-guide](//github.com/sbezludny/javascript-style-guide)


<a name='authors'>Contributors</a>
----------------------------------

- [View Contributors](//github.com/airbnb/javascript/graphs/contributors)


<a name='license'>License</a>
-----------------------------

(The MIT License)

Copyright (c) 2013-2014 REI

Copyright (c) 2012 Airbnb

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

[[↑ back to top]](#TOC)


[airbnb-styleguide]:https://github.com/airbnb/javascript
