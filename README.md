Flounder.js 0.2.0
=================

(for modern browsers and ie9+)

Flounder is a styled select box replacement aimed at being easily configurable while conforming to native functionality and accessibility standards.

```
// npm
require('flounder');

// es6
import Flounder from 'flounder';
```


Usage
=====

Flounder can be used in vanilla js or with react.

```
// vanilla
new Flounder( target, configOptions );

// react
ReactDOM.render( React.createElement( FlounderReact, configOptions ), target );

// react (JSX)
React.render( <FlounderReact option1="" option2="">, target );

// requirejs
requirejs( [ 'flounder' ], function( Flounder )
{
    new Flounder( target, configOptions );
} );

// jQuery plugin
$( '.example--class' ).flounder( configOptions );

// microbe plugin
µ( '.example--class' ).flounder( configOptions )
```


###Available config options

```
{
    defaultValue        : defaultValue,
    classes             : {
        flounder        : 'class--to--give--the--main--flounder--element',
        hidden          : 'class--to--denote--hidden',
        selected        : 'class--to--denote--selected--option',
        wrapper         : 'additional--class--to--give--the--wrapper'
    },
    multiple            : false,
    multipleTags        : true,
    multipleMessage     : '(Multiple Items Selected)',
    onClose             : function( e, valueArray ){},
    onComponentDidMount : function(){},
    onInit              : function(){},
    onOpen              : function( e, valueArray ){},
    onSelect            : function( e, valueArray ){}
    options             : dataObject,
    search              : true
}
```


Building the select box
=======================

select options must be passed as an array of objects

```
[
    {
        text        : 'probably the string you want to see',
        value       : 'return value',
        description : 'a longer description of this option', // optional
        extraClass  : 'extra--classname' // optional
    }
]
```

or an array.
```
[
    'option 1',
    'option 2',
    'option 3'
]
```

in the case of an array, the passed text will be both the text and the value.  There would be no description in this case


all extra properties passed that are not shown here will be added as data attributes for the sake of reference later.  The options can be accessed in the init (before building) as this.options if they need reformatting or filtering.


API
===

These functions are intended for use in the user provided event callbacks
```
destroy()
getOption( num )
getSelectedOptions()
getSelectedValues()
rebuildOptions( options )
disable( bool )
```


Contributing
============

We gladly accept and review any pull-requests. Feel free! :heart:


This project adheres to the [Contributor Covenant](http://contributor-covenant.org/). By participating, you are expected to honor this code.

[Flounder - Code of Conduct](https://github.com/sociomantic/flounder/blob/master/CODE_OF_CONDUCT.md)

Need to report something? [hr@sociomantic.com](hr@sociomantic.com)


Example
========

Given the example options:

```

    var options = [
        {
            cssClass    : 'select-filters',
            id          : 'All',
            isTaxonomy  : true,
            text        : 'All'
        },
        {
            cssClass    : 'category',
            id          : 'category',
            isTaxonomy  : true,
            text        : 'Categories'
        },
        {
            cssClass    : 'tag',
            id          : 'tag',
            isTaxonomy  : true,
            text        : 'Tags'
        }
    ];
```

a vanilla multi-flounder with tags

flounder can be attached to basically anything

```

    new flounder( document.getElementById( 'example' ), {
        defaultValue        : 'placeholders!',

        onInit              : function()
        {
            var res = [];
            options.forEach( function( option )
            {
                res.push( {
                    text        : option.text,
                    value       : option.id
                } );
            } );

            this.options = res;
        },

        multiple            : true } );
```

a react multi-flounder with tags

react flounder can only be attached to container elements (div, span, etc)


```

    ReactDOM.render( React.createElement( FlounderReact, {
        defaultValue        : 'placeholders!',

        multiple            : true,

        onInit              : function()
        {
            var res = [];
            options.forEach( function( option )
            {
                res.push( {
                    text        : option.text,
                    value       : option.id
                } );
            } );

            this.options = res;
        } } ), document.getElementById( 'example' )
    );
```


The result of either of these is shown here (only styled with the structural css)

![closed](https://d1ro8r1rbfn3jf.cloudfront.net/ms_16133/Vu591qbeROU9QezI1cXQ1XkYoQEkhP/Flounder%2Bdemo%2B2015-11-23%2B23-26-41.jpg?Expires=1448404005&Signature=Rj~Hm6GmMgBCFkwr4~BnhmYyrcHDzMYGS9GGIg4kPHgCc7GhMmIStXlFJouWAEny4BeMXKHMZu-ruXTQwRCeVeZf2oL098kTyScHEVLsyZr-JZ6z6mnPP-ikgMlvc78xZJcZsdIjDEihaVm3NmJWRmfq~kKH3BvVQaLgUt7NyZV6IxuRhYfxUFkBlHOg6moHTibrehy-Yvni8fllz8BekBX-oVibZ6ezgmBQvOrOOCGRjp39mn4-QJU8jpNO41RW3iG2osAXJMxlmJhG8cL6X7trpM1VWQP7M462PrtnGt6~j4BjammY8hldEaDp8LpjsCI-2AGOm48FqGH5VAVLPw__&Key-Pair-Id=APKAJHEJJBIZWFB73RSA)

![open menu](https://d1ro8r1rbfn3jf.cloudfront.net/ms_16133/MfbfkOAmsRGZHKfONjpntVYHRLzaUF/Flounder%2Bdemo%2B2015-11-23%2B23-26-20.jpg?Expires=1448403987&Signature=bxaazMlR6YnSqY4-mm8wZ5ZaeiiyHSIcYoptQLlk96DZB3cWM9JRUH6cuvVdbgEpuAwViJgBQPeeDyRBEfql5IS3WJXWPTlFCv-dOwvKT-7VboFDbjPv5-JD1TmBNr4ElcdWGTK8TsISv~8Bo0p35vnXnwUx7LBUTj86z3Z4hEP8-YMkU8vLVaYoqEDy6jSYDtptfTZvMxH3x4Nv2gNOeRLt-RYH9vhQtt1Vqv4YsOF29lNe2EmrvV5VDahdOviuPMwJ4K5HyggGZ4qsO84DM~~KhAS4ff50SCk069cfWRVARYwW1JGm71D-ccmPYQzM70pT1pAMIaqWkFjpFAy8CA__&Key-Pair-Id=APKAJHEJJBIZWFB73RSA)

![1 selected](https://d1ro8r1rbfn3jf.cloudfront.net/ms_16133/mL3upXVlwnB4pkC4jN5QCE4ZIdiQ8F/Flounder%2Bdemo%2B2015-11-23%2B23-26-57.jpg?Expires=1448404020&Signature=bWFxIgxc-0DQWqSAWXCNzGI5R9LiCho7EfuHgUp0wheeDl85cui3OcnOcw~HSYR6sSJ6XcQPHeVE5FAet1suEFR2q0fe9p--tuq8G9T0wK0Mp6fLYi49OGs6mTftFzQy3zgUVlPKY58nIejzAl6N-fT67NjUqKBhfUltjssc-OZvD3TZf7nAS0erQwuiM5QH6y9sFscavZWHDrsV1ReXkYqMbRXtbykM~JNPP-2Pr9ZvRwpcA7wdFpTpIF4OH0SsR-hem-xnnZ1ZHvJELARqzp2Q6OLWapRdaHHg~9OTnIDY7~lbz-2XcmrP6wMLJqZ6bqVuoWfCdtLk8VK6xQdIEg__&Key-Pair-Id=APKAJHEJJBIZWFB73RSA)

See more examples on the [demo page](./demo/index.html)


Public API
==========

```
    destroy()
    getOptions( num )
    getSelectedOptions()
    rebuildOptions( options )
    disable( bool )
```


Change Log
==========

0.2.0
-----

+ user callbacks now keep their name internally for dynamic changes
+ some users callback now give the array of selected values (see examples)
+ _default is now defaultValue
+ the constructor now accepts µ and $ objects and returns an array of flounders
+ a call to the constructor without and arguments now returns the constructor
+ added getSelectedValues() to API
+ added the ability to give options unique classes
+ added wrapper to the class options
+ changed the flounder class optoin from container to flounder
+ restructured folders and files


0.1.5
-----

+ added rebuildOption and getOptions
+ added dynamic options
+ added getSelected
+ fixes in keypress handlers
+ added support for AMD loaders
+ added a jquery plugin wrapper
+ added a microbe plugin wrapper
+ fixed multi-select with dynamic options


0.1.4
-----

+ flounder now detroys itself properly


0.1.3
-----

+ fresh opening a menu now scrolls to selected (non-multiple)
+ events in setValue are now normalized


0.1.0
-----

+ all callback functions all start with `on` for clarity (`init becomes `onInit`)
