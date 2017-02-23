<p align="center"><a href="#" target="_blank"><img width="300px" src="https://www.yhspy.com/view/github/ballpen.js/art.png?v=v0.1.3-alpha"></a></p>

<p align="center">
  <a href="https://circleci.com/gh/Becavalier/Ballpen.js/tree/master"><img src="https://img.shields.io/circleci/project/Becavalier/Ballpen.js/master.svg" alt="Build Status"></a>
  <a href="https://www.npmjs.com/package/ballpen.js"><img src="https://img.shields.io/npm/dt/ballpen.js.svg" alt="Downloads"></a>
  <a href="https://www.npmjs.com/package/ballpen.js"><img src="https://img.shields.io/npm/v/ballpen.js.svg" alt="Version"></a>
  <a href="https://www.npmjs.com/package/ballpen.js"><img src="https://img.shields.io/npm/l/ballpen.js.svg" alt="License"></a>
</p>

## Description
**Ballpen.js** is a lightweight, plugin based mvvm developing framework ready for building flexible web apps. It's very easy to use, and you can get it into your work only after a few minutes's quick learning.

## Installation

``` shell
npm install ballpen.js --save
```

## Quick Start

```html
<!-- html -->
<div id="app">
  <h1 bp-show="header.showTitle">{{ header.title }}</h1>
  <input type="text" bp-model="header.title" bp-event:input="syncTitle"></input>
  <button bp-event:click="foldTitle">
    <span>{{ header.buttonTxt }}</span>
  </button>
</div>
```

```javascript
// javascript
let data = {
    header: {
        showTitle: true,
        title: "It's a sunny day!",
        buttonTxt: "- Fold -"
    }
};

new Ballpen("#app", {
    data: data,
    event: {
        foldTitle: (el, context, args) => {
            context.header.showTitle = !context.header.showTitle;
        },
        syncTitle: (el, context, args) => {
            context.title = el.value;
        }
    },
    watchers: {
        "header": {
            handler: (getter, setter) => {
                if (!getter.showTitle) {
                    setter.$buttonTxt = '- Unfold -';
                } else {
                    setter.$buttonTxt = '- Fold -';
                }
            }
        }
    }
});
```

## Directives

* **bp-model**

> 'bp-model' is used for binding data to a distinct DOM element. For normal DOM element, 'bp-model' will bind data instead of its `innerHTML` attribute. For `<input>` like element, 'bp-model' will bind data instead of its `value` attribute. 'bp-model' will ignore the moustache style template within the DOM label.

> e.g: [examples/bp-model.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-model.html)

* **bp-class**

> 'bp-class' is used for binding DOM elements' class name with distinct data.

> e.g: [examples/bp-class.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-class.html)

* **bp-for**

> 'bp-for' is used for rendering DOM element with `Array` like data, ballpen.js will automatically rendering DOM, copying and binding them to a distinct amount the same as `Array`'s length'.

> e.g: [examples/bp-for.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-for.html)

* **bp-event**

> 'bp-event' is used for binding events to DOM elements.

> e.g: [examples/bp-event.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-event.html)

* **bp-bind**

> 'bp-bind' is used for binding regular or customized attributes to DOM elements.

> e.g: [examples/bp-bind.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-bind.html)

* **bp-pre**

> 'bp-pre' is used for preventing distict DOM element from being rendered by ballpen.js.

> e.g: [examples/bp-pre.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-pre.html)

* **bp-shade**

> 'bp-shade' is used for hiding all of the rendering areas before render is getting done.

> e.g: [examples/bp-shade.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-shade.html)


* **bp-show**

> 'bp-show' is used for hiding or displaying elements according to distinct data's value.

> e.g: [examples/bp-show.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-show.html)

* **bp-ref**

> 'bp-ref' is used for storing DOM elements into a global object `Ballpen.$refs`, you can get native DOM element directly from this global object which you had binded an 'bp-ref' on it before.

> e.g: [examples/bp-ref.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/bp-ref.html)


## Core Features

* **Moustache Template**

> You can use 'Moustache Template' to bind data to DOM elements flexibly, with a data path inside this symbol `{{}}`, ballpen.js will automatically rendering 'Moustache Template' with corresponding data, and make it a 'Two-Way Data Binding'. 

> e.g: [examples/core-moustache.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/core-moustache.html)

* **Data Watcher**

> You can use 'Watcher' to watch your data flow's changes, according to the changes, you can do everything what you want. ****Please take care that you can just set a watcher on an object or an array, not on any single normal data.****

> e.g: [examples/core-watcher.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/core-watcher.html)

* **Lifecycle Hook Point**

> You can inject hook functions at every lifecycle hook points, it's include: "beforeRender", "afterRender".

> e.g: [examples/core-lifecycle.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/core-lifecycle.html)

## Plugin System

### Build-in Plugins

* **Ballpen.$http**

> You can use `Ballpen.$http` to access ajax releatived operations. Based on [axios](https://github.com/mzabriskie/axios)

> e.g: [examples/plugin-$http.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/plugin-$http.html)

* **Ballpen.$cookie**

> You can use `Ballpen.$cookie` to access cookie releatived operations. Based on [js-cookie](https://github.com/js-cookie/js-cookie)

> e.g: [examples/plugin-$cookie.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/plugin-$cookie.html)

* **Ballpen.$cache**

> You can use `Ballpen.$cache` to access local cache releatived operations. Based on [localForage](https://github.com/localForage/localForage)

> e.g: [examples/plugin-$cache.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/plugin-$cache.html)


* **Ballpen.$util**

> You can use `Ballpen.$utl` to access many utility methods, such as `isEmpty`, etc. Based on [underscore](https://github.com/jashkenas/underscore)

> e.g: [examples/plugin-$util.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/plugin-$util.html)


* **Ballpen.$animate**

> You can use `Ballpen.$animate` to make animations on DOM elements as you wish. Based on [velocity](https://github.com/julianshapiro/velocity)

> e.g: [examples/plugin-$animate.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/plugin-$animate.html)


### Third Party Plugins

> You can use `Ballpen.registerPlugin(<alias>, <entity>)` to register third party plugins into Ballpen's global environment, then you can call plugin functions by `Ballpen.$<alias>`.

> e.g: [examples/plugin-registerPlugin.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/plugin-registerPlugin.html)


## Instance Properties

* **.data**

> You can access the 'data' attribute from an constructed instance object. According to this attribute, you can get all the constructing data of the current status.

> e.g: [examples/instance-data.html](https://github.com/Becavalier/Ballpen.js/blob/master/examples/instance-data.html)



## License

[MIT](http://opensource.org/licenses/MIT)

Copyright (c) 2017-present, YHSPY