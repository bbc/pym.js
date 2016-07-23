# Pym.js

## BBC-specific modifications
* We added the ability to init a pym Parent with a sourcedoc attribute rather than an iFrame URL.
* We added a way of accessing host information:
 
1. When creating pym Parent, pass a `config` property with whatever you like (e.g. host URL, cookies, etc)
2. When creating pym Child, pass a `connectedCallback` function, which is invoked once a connection has been made with the pym Parent.
3. Anything inside the callback can safely call pym Child.getHostInformation() - this provides a nice easy way for pym Childs to access host information.

Example:

```js
var myConf = {
    hostInformation: {
        onBbcDomain: true,
        category:    'news'
    },
    applicationHtml: coreContentContainer.innerHTML
};
var pymParent = new pym.Parent(iframeUid, iframeUrl, {config: myConf});
```

...and the child:

```js
new pym.Child({
    polling: 100,
    connectedCallback: function downloadApplication(self) {
        console.log(self.getHostInformation().hostInformation);
    }
});
```

---

The original README is below.

---

## About

Using iframes in a responsive page can be frustrating. It&rsquo;s easy enough to make an iframe&rsquo;s width span 100% of its container, but sizing its height is tricky &mdash; especially if the content of the iframe changes height depending on page width (for example, because of text wrapping or media queries) or events within the iframe.

<a href="https://raw.githubusercontent.com/nprapps/pym.js/master/src/pym.js">Pym.js</a> embeds and resizes an iframe responsively (width and height) within its parent container. It also bypasses the usual cross-domain issues.

Use case: The NPR Visuals team uses Pym.js to embed small custom bits of code (charts, maps, etc.) inside our CMS without CSS or JavaScript conflicts. [See an example of this in action.](http://www.npr.org/2014/03/25/293870089/maze-of-college-costs-and-aid-programs-trap-some-families)

### [&rsaquo; Read the documentation](http://blog.apps.npr.org/pym.js/)

### [&rsaquo; Browse the API](http://blog.apps.npr.org/pym.js/api/)

## Development tasks

Grunt configuration is included for running common development tasks.

Javascript can be linted with [jshint](http://jshint.com/):

```
grunt jshint
```

Unminified source can be regenerated with:

```
grunt concat
```

Minified source can be regenerated with:

```
grunt uglify
```

API documention can be generated with [jsdoc](https://github.com/jsdoc3/jsdoc):

```
grunt jsdoc
```

The release process is documented [on the wiki](https://github.com/nprapps/pym.js/wiki/Release-Process).

## License & Credits

Released under the MIT open source license. See `LICENSE` for details.

Pym.js was built by the [NPR Visuals](http://github.com/nprapps) team, based on work by the [NPR Tech Team](https://github.com/npr/responsiveiframe) and [Ioseb Dzmanashvili](https://github.com/ioseb). Thanks to [Erik Hinton](https://twitter.com/erikhinton) for suggesting the name.

Additional contributors:

* [Pierre-Yves Jamon](https://github.com/Pym)
* [jugglinmike](https://github.com/jugglinmike)
* [David Rogers](https://github.com/al-the-x)
* [Noah Veltman](https://github.com/veltman)
* [Andrei Scheinkman](https://github.com/ascheink)
* [Thomas Wilburn](https://github.com/thomaswilburn)
* [Justin Dearing](https://github.com/zippy1981)
* [Chris Amico](https://github.com/eyeseast)
* [Ryan Murphy](https://github.com/rdmurphy)
