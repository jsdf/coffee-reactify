# coffee-reactify

# STATUS: DEPRECATED

This tool is no longer maintained. If you need to transition your codebase from
it, a codemod is available to do so: [cjsx-codemod](https://github.com/jsdf/cjsx-codemod)

This project started as a way for me to explore how JSX could fit into
Coffeescript syntax, as a quickly hacked together prototype. While I never
really promoted it, it quickly took on a life of its own, and before long people
were asking for it to support all kinds of different use cases. On top of that I
had no experience writing parsers, so the result is something with 
[insurmountable limitations](https://github.com/jsdf/coffee-react/issues/32).

As I eventually stopped using Coffeescript I ended up neglecting this project,
but as people were using it I didn't want to kill it. I really should have,
however, because it meant that people were using a crappy, ill-conceived,
unmaintained tool. Now, long overdue, I'm putting it out to pasture.

Original readme follows:

browserify v2 plugin for compiling [coffee-react-transform](https://github.com/jsdf/coffee-react-transform) CJSX markup in Coffeescript.

# example

given some files written in a mix of `coffee` and `cjsx`:

neat-ui.coffee:
``` coffee
require './rad-component.cjsx'

React.renderComponent RadComponent({rad:"mos def"}),
	document.getElementById('container')
```

rad-component.cjsx:
``` coffee
# @cjsx React.DOM 

React = require('react')

RadComponent = React.createClass
  render: ->
    <div className="rad-component">
      <p>is this component rad? {@props.rad}</p>
    </div>
```

install coffee-reactify:

```bash
$ npm install -g coffee-reactify
```

version compatibility: 

- 2.1.x - React 0.12.1
- 2.x - React 0.12
- 1.x - React 0.11.2
- 0.x - React 0.11 and below

when you compile your app, pass `-t coffee-reactify` to browserify:

```bash
$ browserify -t coffee-reactify neat-ui.coffee > bundle.js
```

you can omit the `.coffee` or `.cjsx` extension from your requires if you add the extension to browserify's module extensions:

``` coffee
require './component'
...
```

```bash
$ browserify -t coffee-reactify --extension=".cjsx" --extension=".coffee" neat-ui.coffee > bundle.js
```

providing the transform option `coffeeout: true` will passthrough the transformed
output of `.coffee` files with the `@cjsx` pragma without compiling them to javascript.
this means you can use a different coffee compiler transform such as [icsify](https://github.com/maxtaco/icsify) or [coffeeify](https://github.com/jnordberg/coffeeify) in conjunction with this transform.

**note:** at this stage, `.cjsx` files will still be compiled even with `--coffeeout`.
this is a workaround for the fact that other transform modules like `coffeeify` will
ignore `.cjsx` files due to the different file extension.

```bash
$ browserify -t [ coffee-reactify --coffeeout ] -t coffeeify neat-ui.coffee > bundle.js
```

# install

With [npm](https://npmjs.org) do:

```bash
npm install coffee-reactify
```

# license

MIT
