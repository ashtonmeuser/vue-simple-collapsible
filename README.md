# vue-simple-collapsible

A simple animated collapsible Vue component.

## Installation

run `npm install --save vue-simple-collapsible`.

## Usage

Import the component using `import Collapsible from 'vue-simple-collapsible';`.

Within your app or parent component, register the collapsible component with `components: { Collapsible }`.

Include the component with a `v-if` condition using `v-if="shouldDisplayCollapsible"`. Note that `shouldDisplayCollapsible` should be replaced with a boolean relevant to your application state.

## Options

The component has three configurable options that can be set by specifying component properties. They are `duration`, `delay`, and `easing`. The `duration` and `delay` properties must be numbers and represent the animation duration in seconds and animation delay in seconds, respectively. The `easing` property must be a valid CSS animation timing function (see [documentation](https://www.w3schools.com/cssref/css3_pr_animation-timing-function.asp)).

## Example

A very basic example application displaying the collapsible component's ability to animate collapsing and expanding. Also displays the component's ability to return to a dynamic height after the animation has completed.

```
<template>
  <div class="container">
    <Collapsible
      v-if="open"
      :duration="0.2"
      :delay="0.0"
      easing="ease-out">
      <div class="test-content">
        <div
          v-for="key in text"
          :key="key">
          {{ key }}
        </div>
      </div>
    </Collapsible>
    <button @click="open = !open">
      Toggle Visibility
    </button>
    <button @click="text.push(`String ${text.length}`)">
      Add Child
    </button>
  </div>
</template>

<script>
import Collapsible from 'vue-simple-collapsible';

export default {
  components: {
    Collapsible,
  },
  data: () => ({
    text: ['Hello, World'],
    open: false,
  }),
};
</script>

<style>
.test-content {
  background-color: pink;
}
</style>

```
