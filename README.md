image-progress
=========

A wrapper for loading image via XHR and dispatching progress events.

## How to use

### 1. Install the plugin.
With npm:
```
npm i image-progress --save
```

With Component(1):
```
component install ayamflow/image-progress
```

### 2. Use

```
var Progress = require('image-progress');

var img = new Progress('test-img.png');

img.on('error', function(event) {
    console.log('there has been an error', event);
});

img.on('progress', function(event) {
    console.log('The image is ' + event.progress * 100 + '% loaded !', event.loaded, event.total, event.progress);
});

img.on('load', function(event) {
    console.log('The image is loaded.');
});

img.on('start', function(event) {
    console.log('The image with URL ' + event.url + ' has started loading');
});

img.load();
```

By default, the `event.progress` only has 2 decimals. You can set the number of decimals by setting the `leading` property like this: `imgProgress.leading = 4;`

## Methods
* ### `new Progress(url, params)`

`url`: the URL for the image you want to load.

`params`: the params hash is used if you need to store & retrieve any property on the `start` & `load` events.

* ### `load()`

Starts the loading. It will fire a `start` event.

* ### `destroy()`

Removes all internal & external listeners, and clears the XHR object.

By default, this method is called after the `load` and/or `error` events are triggered. you can disable this behavior by setting `progress.autoclear = false;`

## Properties
* ### `leading` (default: 2)

The number of decimals in the `event.progress` property.

* ### `autoclear` (default: true)

Set wether the `destroy` method should be automatically called after a `load` or `error` event.


## Events
* `start`: fired when the loading starts. The event contains a reference to the `params` hash, as well as the `url`.
* `progress`: fired each time the XHR request updates. The event has 3 properties: `loaded`, `total` and `progress`.
* `load'`: fired when the loading is complete. The event contains a reference to the `params` hash, as well as the `url`.
* `error`: fired when a network-related error is raised.