# Mastering Vuex

[The course is available here](https://www.vuemastery.com/courses/mastering-vuex).

## Intro to Vuex

- State is the single source of truth.
- Let's compare the Vue instance to Vuex:

| Vue instance | Vuex    |
| ------------ | ------- |
| data         | state   |
| methods      | actions |
| computed     | getters |

The store has also `mutations` called by `actions` to update the `store` to ease the debugging.

## Mastering Vuex Orientation

Checkout the [Real World Vue course](../Real.world.vue2.course/Notes.md).

## State & Getters

### How to use the state from the vue

Either a direct access:

```js
default {
  computed: {
    userName() {
      return this.$store.state.user.name;
    },
    userID() {
      return this.$store.state.user.id;
    },
  },
};
```

Or `mapState`:

```js
import { mapState } from 'vuex';

export default {
  computed: mapState({
    userName: (state) => state.user.name,
    userID: (state) => state.user.id,
    categories: (state) => state.categories,
  }),
};
//OR without dot notation
export default {
  computed: mapState({
    user: 'user',
    categories: 'categories',
  }),
};
```

Or even, without naming the computed properties:

```js
import { mapState } from "vuex";

export default {
  computed: mapState(["user", "categories"]),
};
```

All three solutions give the same output.

### How to use local compare properties with `mapState`

Use the spread operator:

```js
import { mapState } from "vuex";

export default {
  computed: {
    localComputed() {
      return "My local computed!";
    },
    ...mapState(["user", "categories"]),
  },
};
```

### What about getters

They are stored in the store.

We can do the same thing with the getters using `mapGetters`.

```js
import { mapState, mapGetters } from "vuex";

export default {
  computed: {
    ...mapGetters(["categoryCount"]),
    ...mapState(["user", "categories"]),
  },
};
```

## Mutations & Actions Part 1

- Mutations update the data
  - Mutations are named in capitals as a convention. It is not mandatory but highly recommanded.
- Actions retrieve the data from an API and pass it on to mutations using `commit('MUTATION_NAME', someValue)`.
- The component triggers an action using `this.$store.dispatch('actionName', this.payload)`.

## Mutations & Actions Part 2

To reload a component when the url changes, including query strings, use this:

```html
<!-- Reload the component when the url change -->
<router-view :key="$route.fullPath" />
```

## Modules

- They allow to organize the state.
- We can use modules for:

  - data models (ex: user vs event)
  - feature (ex: cart vs product inventory)

### 2 ways to organize state and modules

#### Method 1

The module:

```js
export const state = {...}
export const actions = {...}
export const mutations = {...}
export const getters = {...}
```

then import it with:

```js
import * as storeModule from "/path/to/store/module";
```

#### Method 2

The module:

```js
export const default {
  state: {...},
  actions: {...},
  mutations: {...},
  getters: {...}
};
```

then import it with;

```js
import storeModule from "/path/to/store/module";
```

### How to access state of modules between each other

For example, in an action :

```js
const actions = {
  saveEvent({ commit, rootState }, event) {
    console.log(`User ${rootState.user.user.name} is creating an event`);
    return EventService.postEvent(event).then(() => {
      //only commit if the backend has saved the data
      commit("ADD_EVENT", event);
    });
  },
};
```

### How to call module actions from another

For example, in an action :

```js
const actions = {
  saveEvent({ commit, dispatch, rootState }, event) {
    console.log(`User ${rootState.user.user.name} is creating an event`);
    dispatch("userActionToCall"); //CALLED WITHOUT THE MODULE NAME
    return EventService.postEvent(event).then(() => {
      //only commit if the backend has saved the data
      commit("ADD_EVENT", event);
    });
  },
};
```

### Namespacing modules

It can be done simply with `namespaced = true`.

So with an example with actions:

```js

export default {
  methods: mapActions(["event/fetchEvent"]), //namespaced array of actions
}
export default {
  methods: mapActions("event", ["fetchEvent"]), //namespace + array of actions
}
```

It works the same for getters.

So taking the example above, in an action, do we need to change any code?

```js
const actions = {
  saveEvent({ commit, dispatch, rootState }, event) {
    //=> NO
    console.log(`User ${rootState.user.user.name} is creating an event`);
    //NO if the Action is inside the current module, OTHERWISE, use
    dispatch("userActionToCall");
    //null => payload but could be any object.
    //dispatch("user/ActionToCall", null, {rout: true});
    return EventService.postEvent(event).then(() => {
      //only commit if the backend has saved the data
      commit("ADD_EVENT", event); //NO if the Mutation is inside the current module.
    });
  },
};
```

**BEST PRACTICE**: do not call mutations from other modules, **use their action**.

## Success & Error notifications

It is just putting into application the vuex module principle.
