# react-dom-utils

[![npm](https://img.shields.io/npm/v/react-dom-utils.svg)](https://www.npmjs.com/package/react-dom-utils)
[![Travis](https://img.shields.io/travis/wuct/react-dom-utils.svg)](https://travis-ci.org/wuct/react-dom-utils)
[![Codecov](https://img.shields.io/codecov/c/github/wuct/react-dom-utils.svg)](https://codecov.io/github/wuct/react-dom-utils)
[![Code Climate](https://img.shields.io/codeclimate/github/wuct/react-dom-utils.svg)](https://codeclimate.com/github/wuct/react-dom-utils)

Inspired [recompose](https://github.com/acdlite/recompose/), [react-dom-utils](https://www.npmjs.com/package/react-dom-utils) let you work with DOMs in HOCs.

## Installation

`npm install react-dom-utils --save`

## API

Docs are annotated using Flow type notation, given the following types:

```js
type ReactElementType = Class<ReactComponent> | StatelessFunctionComponent | string
```

### `mapPropsOnEvent()`

```js
mapPropsOnEvent(
  getTarget: (component: ReactComponent) => DOMEventTarget
  type: string,
  propsMapper: (event: DOMEvent, component: ReactComponent) => Object,
  throttle: Function,
  mapOnMount: boolean,
  BaseComponent: ReactElementType
): ReactElementType
```

Attaches the props returned by `propsMapper` to owner props and updates it when the specified event is triggered.

### `withMousePosition()`

```js
withMousePosition(
  throttle: Function
): ReactElementType
```

Attaches `mousePosition` to owner props and updates it when a `mouseover` event of the base component is triggered.

`mousePosition` has the following signature: 

```js
{
  pageX: number,
  pageY: number,
  clientX: number,
  clientY: number,
  screenX: number,
  screenY: number
}
```

### `withSize()`


```js
withSize(
  throttle: Function
): ReactElementType
```

Attaches `DOMSize` to owner props and updates it when a `resize` event (detected by [element-resize-detector](https://github.com/wnr/element-resize-detector)) of the base component is triggered.

`DOMSize` has the following signature: 

```js
{
  offsetWidth: number,
  offsetHeight: number,
  clientWidth: number,
  clientHeight: number,
  scrollWidth: number,
  scrollHeight: number
}
```
 
### `withWindowSize()`

```js
withWindowSize(
  throttle: Function
): ReactElementType
```

Attaches `windowSize` to owner props and updates it when a `resize` event of `window` is triggered.

`windowSize` has the following signature: 

```js
{
  innerWidth: number,
  innerHeight: number,
  outerWidth: number,
  outerHeight: number
}
```

### `withOffsetToRoot()`


```js
withOffsetToRoot(
  throttle: Function
): ReactElementType
```

Attaches `offsetToRoot` to owner props and updates it when a `resize` event of `window` is triggered.

`offsetToRoot` has the following signature: 

```js
{
  offsetTop: number,
  offsetLeft: number
}
```
 
## Usage
### `throttle`
Throttling functions are used for throttling events. All throttle functions are default to [lodash/identity](https://lodash.com/docs#identity). In other words, there is no throttling by default. It is recommended to use [raf-throttle](https://github.com/wuct/raf-throttle) instead.

## Example

```js
import React from 'react'
import throttle from 'raf-throttle'
import withMousePosition from 'react-dom-utils/lib/withMousePosition.js'

export default withMousePosition(throttle)(
  ({ mousePosition }) => <div>{JSON.stringify(mousePosition)}</div>
)
```

More examples is [here](https://github.com/wuct/react-dom-utils/tree/master/example)

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
