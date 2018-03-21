Outline a element in Vue on focus or hover using the hand-drawn style of roughjs.

![Example of sketch-outline in action. A cursor hovers over links that read "Sample Link" and a hand-drawn box appears when the link is hovered.](https://raw.githubusercontent.com/SaFrMo/sketch-outline/master/demo.gif)

# Usage

`npm install sketch-outline --save`

```js
// Import and register the component in your main JS file
import SketchOutline from 'sketch-outline'
Vue.component('sketch-outline', SketchOutline)
```

```
<template>
    <!-- Then use in a template -->
    <sketch-outline color="#c00">
        <h1>Red outline on hover</h1>
    </sketch-outline>
</template>
```

# Props
* `color`, string, default `#c00`. Color of the border.
* `padding`, number, default `20`. Pixels of padding to give the sketch outline.

# Contributing
Questions and issues welcome!
