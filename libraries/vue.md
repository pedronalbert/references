# VueJS
<!-- TOC -->

- [VueJS](#vuejs)
    - [Component](#component)
        - [Props](#props)
        - [Computed Properties](#computed-properties)
        - [Watch](#watch)
        - [Event Dispatch](#event-dispatch)
    - [Template](#template)
        - [Binding](#binding)
            - [Property Binding](#property-binding)
            - [Event Handler](#event-handler)
                - [Modifiers](#modifiers)
        - [Dinamyc Component](#dinamyc-component)
        - [Slots](#slots)
            - [Named Slot](#named-slot)
        - [KeepAlive](#keepalive)
        - [Conditional](#conditional)
            - [v-if](#v-if)
            - [v-show](#v-show)
        - [List](#list)
    - [Froms](#froms)
        - [v-model](#v-model)
            - [Modifies](#modifies)

<!-- /TOC -->
## Component
```js
export default {
  name: 'MyComponent',

  data() {
    return {
      // ...
    };
  },
};
```

### Props
```js
{
  props: ['title'],
  props: {
    title: {
      type: [String, Number],
      required: true,
      validator(value) {
        // ...
      },
    },
  },
};
```

### Computed Properties
```js
{
  computed: {
    average() {
      // ...
    },

    fullName() {
      get() {
        // ...
      },

      set(val) {
        // ...
      },
    }
  },
}
```
### Watch
```js
{
  watch: {
    avergage(val, oldVal) {
      // ...
    } ,
  },
}
```

### Event Dispatch
```js
{
  methods: {
    delete() {
      this.$emit('delete-user', this.user);
    },
  },
};
```
## Template
### Binding
```html
<p>{{ msg }}</p>
```

#### Property Binding
```html
:href="href"
:class="{ active: isActive }"
:class="[activeClass, errorClass]"
:class="[isActive ? activeClass : errorClass]"
:style="styleObj"
:style="[baseStyle, overStyles]"
```

#### Event Handler
```html
@click="onClick"
@click="onClick(user)"
@click="onClick($event)"
@click="count += 1"
```
##### Modifiers
```html
.stop
.prevent
.capture
.self
.once
.passive
```

### Dinamyc Component
```html
<component :is="componentName">
```

### Slots
```html
<component>
  <slot></slot>
</component>
```

#### Named Slot
```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>

<!-- Usage -->
<base-layout>
  <template slot="header">
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>

  <template slot="footer">
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

### KeepAlive
Keep component state
```html
<keep-alive>
  <my-component></my-component>
</keep-alive>
```


### Conditional
#### v-if
```html
<p v-if="condition"></p>
<p v-else-if="condition"></p>
<p v-else></p>
```

#### v-show
```html
<p v-show="condition"></p>
```

### List
```html
<li v-for="user in users"></li>
<li v-for="(user, index) in users"></li>
```

## Froms
### v-model
```html
<input v-model="firstName" />
```

#### Modifies
```html
.lazy
.number
.trim
```
