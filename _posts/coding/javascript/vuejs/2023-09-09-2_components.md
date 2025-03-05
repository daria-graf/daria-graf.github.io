---
layout: post
title: 'VueJS Components'
date: 2023-09-09 22:02:00 +0200
categories: VueJs
author: 'Daria Graf'
---

# Components

## Add a new component

```js
// main.js

import { createApp } from 'vue';
import App from './App.vue';
import FriendContact from './components/FriendContact.vue';

const app = createApp(App);
app.component('friend-contact', FriendContact);
app.mount('#app');

// App.vue
<friend-contact></friend-contact>;
```

## Adding Properties to a Component (Parent-Child-Communication)

```js
// ChildComponent.vue

export default {
  props: ['name', 'phoneNumber', 'emailAdress'],
  data() {
    return {},
    };
  },
  methods: {},
  },
};

// ParentComponent.vue
<friend-contact name="Manuel Kirscher"
  phone-number="1234 3555" email-adress="m.k@example.com"
></friend-contact>

```

The Props of a component should not be mutated. If we try to modify component's properties inside the component itself and not outside (e.g. in the parent component) - we will get a compiler error "Unexpected mutation of 'foo' property". This concept is called in Vue **unidirectional data** flow (one-way data flow).
In order to be able to modify the incoming values, we can use the following approach:

1. create a new data property and set its value to the incoming prop's value

```js
props: ["isFavouriteProdukt"],
data(){
    isFavourite: this.isFavouriteProdukt
}
```

## Prop Validation

```js
props: {
    name: {
        type: String,
        required: true
    },
    surname: {
        type: String,
        required: true
    },
    lovesDogsOrCats: {
        type: String,
        // other possible types:
        // String, Number, Boolean, Array, Object
        // Date, Function, Symbol
        required: false,
        default: false // can also be a function
        validator: function(value){
            return value === 'dogs' || value === 'cats'
        }
    }
}

```

## Dynamic Prop Values

When we are using a different type then a String, we need to write v-bind: or just ":" before the property:

```js
<my-component v-bind:liked='true'></my-component>
```

## Emiting Custom Events (Child-Parent-Communication)

In the Child Component we must emit an event.

```js
// ChildComponent.vue
<template>
...
<button @click="toggleLiked">Like</button>
</template>

<script>
...
 methods: {
  toggleLiked(){
  // we can call a build in emit-method
  // the method must have at least a name of the custom event as a parameter
   this.$emit('toggle-liked', this.id)
  }
  ...
 }
</script>
```

In the Parent Component we listen to the child's events, by using `v-on` or `@` and define methods, which must be executed, when an event has been triggered.
The emitted changed properties of the child will be automatically passed back into the child component.

```html
// ParentComponent.vue
<template>
 <ul>
  <child-component v-for="child in children"
   :key="child.id"
   :is-liked="child.isLiked"
   :id="child.id"
   @toggle-liked="updateLikedStatus" // or v-on:toggle-favourite
   >
  </child-component>
 </ul>
</template>

<script>
...
 methods: {
  updateLikedStatus(childId){
   const childToUpdate = this.children.find(child => child.id === childId);
   childToUpdate.isLiked = !childToUpdate.isLiked;
  }
  ...
 }
</script>
```

## Custom Event Definition

We use `emits`-property in order to communicate, which events a component will emit.

```html
<script>
  props: {...},
  emits:['toggle-favourite'],
  data(){
  ...
  }
</script>
```

## Custom Event Validation

```html
// ChildComponent.vue ...
<script>
  props: {...},
  emits: {
      'toggle-liked': function(id){
          return id ? true : {console.warn("id is missing); false};
      }
  }
  data(){
  ...
  }
</script>
```

## Direct Communication between Children Components

### Event Bus [VUE 2]

Event Bus is equal to a Service in Angular.
This Concept is not used anymore in Vue 3. Instead provide/inject or Global state management, such as Vuex (opens new window) should be considered. See https://v3.vuejs.org/guide/migration/events-api.html#event-bus.

```js
// main.js
export const eventBus = new Vue();

--- alternative code ---
export const eventBus = new Vue({
    methods: {
        editStatus(status){
            this.$emit('status-changed', status);
        }
});
--- end ---

// MyComponent.vue
<script>
    import {eventBus} from '../main';

    export default {
        ...
        methods: {
            editStatus() {
            this.status = 'New Status';
            eventBus.$emit('status-changed', this.status);
        }
        ...
    }

</script>

// SomeComponent.vue
<script>
    import {eventBus} from '../main';

    export default {
        ...
        methods: {
        },
        created() {
            eventBus.$on('status-changed', (data) => {
                this.status = data;
            });
        },
        beforeDestroy() {
            // removing eventBus listener
            eventBus.$off('status-changed');
        }
    }

</script>
```

### Slots

Slots are used to customize the html-code content inside a child component.

```html
// SomeComponent.vue

<template>
  <app-note>
    <p>{{text}}</p>
  </app-note>
</template>

<script>
  import AppNote from './components/AppNote.vue';

  export default {
    data() {
      return {
        text: 'A simple note',
      };
    },
    components: {
      appNote: AppNote,
    },
  };
</script>

// AppNote.vue

<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
  export default {};
</script>

<style scoped>
  div {
    border: 3px solid #333;
    ...;
  }
</style>
```

### Default Content

visit [external link](https://vuejs.org/v2/guide/components-slots.html#Fallback-Content){:target="\_blank"}
visit [external link](https://v3.vuejs.org/guide/component-slots.html#fallback-content){:target="\_blank"}

### Named slots

visit [external link](https://vuejs.org/v2/guide/components-slots.html#Named-Slots){:target="\_blank"}
visit [external link](https://v3.vuejs.org/guide/component-slots.html#render-scope){:target="\_blank"}

## Dynamic Components

```js
<component v-bind:is='currentComponent'></component>
```

When loading a dynamic component, it will be destroyed and created each time it is loaded.
In order to cache a component, we should use a <keep-alive> wrapper element.
For more information, visit: [external link](https://vuejs.org/v2/guide/components-dynamic-async.html){:target="\_blank"}
