# Vuetagger

Simple tag component for Vue.js 1.* and 2.0

## Usage

The `<template>`

```html
<vuetagger :value="tags" @change="updateTags"></vuetagger>
```

On your `<script>`

```javascript
export default {

  components: {
    vuetagger: require('./Vuetagger')
  },

  data() {
    return {
      tags: []
    }
  },

  methods: {
    updateTags(tags) {
      console.log(tags)
    }
  }

}
```

### Regex Pattern (optional)

You could add a regex pattern to the attribute.
If the regex pattern does not match, the new tag wouldn't be added.

Here is the example with regex pattern I've taken from http://emailregex.com/

```html
<vuetagger
  :value="tags"
  @change="updateTags"
  pattern="^[-a-z0-9~!$%^&*_=+}{\'?]+(\.[-a-z0-9~!$%^&*_=+}{\'?]+)*@([a-z0-9_][-a-z0-9_]*(\.[-a-z0-9_]+)*\.(aero|arpa|biz|com|coop|edu|gov|info|int|mil|museum|name|net|org|pro|travel|mobi|[a-z][a-z])|([0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}))(:[0-9]{1,5})?$"
></vuetagger>
```

## License

MIT @ [Mulia Arifandi Nasution](http://mul14.net)
