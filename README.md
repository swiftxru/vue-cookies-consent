# Vue Cookies Consent
![Size](https://img.shields.io/bundlephobia/minzip/@norvikit/vue-cookies-consent)
![Downloads](https://img.shields.io/npm/dt/@norvikit/vue-cookies-consent)
![Version](https://img.shields.io/npm/v/@norvikit/vue-cookies-consent)

Nice and clean Vue component to display message about cookies
- 🎬 [Demo](https://norvikit.github.io/vue-cookies-consent/)

## 📦 Installation

### NPM

`npm install --save @norvikit/vue-cookies-consent`

### Yarn

`yarn add @norvikit/vue-cookies-consent`

## 🚀 Usage in Vue Components

```vue
<template>
  <vue-cookies-consent>
    <template #title>Some default title for window</template>
    <template #description>
      <p>Some description in window</p>
    </template>
    <template #button>Accept cookies</template>
  </vue-cookies-consent>
</template>

<script>
  import VueCookiesConsent from '@norvikit/vue-cookies-consent'
  export default {
    components: {
      VueCookiesConsent
    }
  }
</script>
```

## 🚀 Usage throughout the Vue project
Add this content to main.js
```js
import Vue from "vue";
import VueCookiesConsent from "@norvikit/vue-cookies-consent";
Vue.use(VueCookiesConsent)
```

## 🚀 Usage in Nuxt.js
Create a file `plugins/vue-cookies-consent.js` with the following content:
```js
import Vue from "vue";
import VueCookiesConsent from "@norvikit/vue-cookies-consent";
Vue.use(VueCookiesConsent)
```
Then add plugin to `nuxt.config.js`

```js
plugins: [
    {
      src:"plugins/vue-cookies-consent.js", mode:'client'
    }
]
```

## 🔧 Props

| Prop                  | Type    | Description                                                 | Example                             |
|-----------------------|---------|-------------------------------------------------------------|-------------------------------------|
| colorTitle            | String  | Color of window title                                       | `color-title="#000000"`             |
| colorDescription      | String  | Color of window description                                 | `color-description="#000000"`       |
| colorButton           | String  | Color of button text                                        | `color-button="#FFFFFF"`            |
| backgroundWindow      | String  | Background of window                                        | `background-window="#FFFFFF"`       |
| backgroundButton      | String  | Background of button                                        | `background-button="#C11E31"`       |
| backgroundButtonHover | String  | Background of button on hover state                         | `background-button-hover="#de2b40"` |
| hasShadow             | Boolean | Window has shadow                                           | `:has-shadow="true"`                |
| borderRadius          | Number  | Border radius of window in px                               | `:border-radius="16"`               |
| offsetY               | Number  | Offset of window by Y in px                                 | `:offset-y="16"`                    |
| offsetX               | Number  | Offset of window by X in px                                 | `:offset-x="16"`                    |
| position              | String  | Position of window: `top` or `bottom`                       | `position="top"`                    |
| saveMethod            | String  | Method to save window state after accept: `ls` or `cookies` | `save-method="cookies"`             |

## 🔧 Events

| Event         | Description                                    | Example                       |
|---------------|------------------------------------------------|-------------------------------|
| shown         | Fired after window is shown                    | `@shown="someMethod"`         |
| accept        | Fired after accept button is clicked           | `@accept="someMethod"`        |
| lsSaved       | Fired after window state saved to localStorage | `@ls-saved="someMethod"`      |
| cookiesSaved  | Fired after window state saved to Cookies      | `@cookies-saved="someMethod"` |
| hidden        | Fired after window is hidden                   | `@hidden="someMethod"`        |