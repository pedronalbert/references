# VueJS
<!-- TOC -->autoauto- [VueJS](#vuejs)auto  - [Component](#component)auto    - [Props](#props)auto    - [Computed Properties](#computed-properties)auto    - [Watch](#watch)auto    - [Ref](#ref)auto    - [Provide & Inject](#provide--inject)auto    - [Event Dispatch](#event-dispatch)auto    - [Mixins](#mixins)auto    - [Custom Directive](#custom-directive)auto      - [Hooks](#hooks)auto  - [Template](#template)auto    - [Binding](#binding)auto      - [Property Binding](#property-binding)auto      - [Event Handler](#event-handler)auto        - [Modifiers](#modifiers)auto    - [Dinamyc Component](#dinamyc-component)auto    - [Slots](#slots)auto      - [Named Slot](#named-slot)auto    - [KeepAlive](#keepalive)auto    - [v-once](#v-once)auto    - [Conditional](#conditional)auto      - [v-if](#v-if)auto      - [v-show](#v-show)auto    - [List](#list)auto  - [Froms](#froms)auto    - [v-model](#v-model)auto      - [Modifies](#modifies)auto  - [Animating](#animating)auto    - [Transition](#transition)auto      - [Hooks](#hooks-1)auto      - [Transition on Init](#transition-on-init)auto      - [List Entering/Leaving](#list-enteringleaving)auto      - [Caveats](#caveats)auto    - [CSS Animation](#css-animation)auto  - [Plugin](#plugin)auto  - [Filters](#filters)auto    - [Usage](#usage)auto  - [Cookbook](#cookbook)auto    - [Event Bus](#event-bus)autoauto<!-- /TOC -->
## Component
```js
export default {
  name: 'MyComponent',

  data() {
    return {
      // ...
    };
  },

  // Definitions...
};
```

### Props
```js
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
```

### Computed Properties
```js
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
```
### Watch
```js
watch: {
  avergage(val, oldVal) {
    // ...
  } ,
},
```
### Ref
```html
<my-component ref="myComponent">
```
```js
this.$refs.myComponent
```

### Provide & Inject
Allos us to specfify the data/methods we want to provide to descendent components
```js
// ParentComponent
provide() {
  return {
    myData: data,
  };
},

// ChildComponent
inject: ['myData']
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

### Mixins
```js
const myMixin = {
  methods: {
    //...
  },
};

// component definition
mixins: [myMixin]
```

### Custom Directive
```js
Vue.directive('foo', {
  // ...hooks
})

// shorthand
Vue.directive('foo', (el, binding) => {
  // ...
});
```

#### Hooks
```js
{
  bind() {},
  inserted() {},
  update() {},
  componentUpdated() {},
  unbind() {}
}
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

##### Hooks Events
We can also listen to vue-component hooks

```html
@hook:mounted="onMounted"
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

### v-once
Evaluated once and cached
```html
<div v-once>
  <!-- ... a lot of content -->
</div>
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

## Animating
### Transition
```html
<transition
  name="fade"
  enter-class="class"
  enter-active-class="class"
  enter-to-class="class"
  leave-class="class"
  leave-active-class="class"
  mode="out-in|in-out"
  :duration="1000"
  :duration="{ enter: 500, leave: 1000}"
>
  <my-compontent v-if="show">
</transition>
```

#### Hooks
[Docs](https://vuejs.org/v2/guide/transitions.html#JavaScript-Hooks)
```html
@before-enter="handler"
@enter="handler"
@after-enter="handler"
@enter-cancelled="handler"

@before-leave="handler"
@leave="handler"
@after-leave="handler"
@leave-cancelled="handler"
```
```js
methods: {
  beforeEnter(el) {},
  enter(el, done?) {},
  afterEnter(el) {},
  enterCancelled(el) {}

  beforeLeave(el) {},
  leave(el, done?) {},
  afterLeave(el) {},
  leaveCancelled(el) {}
}
```

#### Transition on Init
```html
<transition appear>

<transition
  appear
  appear-class=""
  appear-to-class=""
  appear-active-class=""

  @before-appear=""
  @appear=""
  @after-appear=""
  @appear-cancelled=""
>
```

#### List Entering/Leaving
> Transition Group add the v-move class when move elements
```html
<transition-group name="fade">
  <!-- v-for -->
</transition>
```

#### Caveats
> When toggling between elements that have the same tag name, you must tell Vue that they are distinct elements by giving them unique key attributes. Otherwise, Vue’s compiler will only replace the content of the element for efficiency. Even when technically unnecessary though, it’s considered good practice to always key multiple items within a <transition> component.


### CSS Animation
CSS animations are applied in the same way as CSS transitions, the difference being that v-enter is not removed immediately after the element is inserted


![Transition CSS Timeline](https://vuejs.org/images/transition.png)

## Plugin
```js
const MyPlugin = {
  install(Vue, options) {
    Vue.globalMethod() {},
    Vue.directive('foo', {}),
    Vue.mixin({}),
    Vue.prototype.$myMethod() {},
  },
};

// usage
Vue.use(MyPlugin);
```

## Filters
>You can define local filters in component definition
```js
Vue.filter('foo', (value, arg) => {

});
```

### Usage
```html
{{ message | filter }}
<div :id="id | filter('arg')">
```

## Cookbook

### Event Bus
```js
const bus = new Vue();

bus.$emit(...);
bus.$on(...);
```