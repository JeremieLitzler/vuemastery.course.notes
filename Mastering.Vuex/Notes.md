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
import { mapState } from 'vuex';

export default {
  computed: mapState(['user', 'categories']),
};
```

All three solutions give the same output.

### How to use local compare properties with `mapState`

Use the spread operator:

```js
import { mapState } from 'vuex';

export default {
  computed: {
    localComputed() {
      return 'My local computed!';
    },
    ...mapState(['user', 'categories']),
  },
};
```

### What about getters

They are stored in the store.

## Mutations & Actions Part 1

## Mutations & Actions Part 2

## Modules

## Success & Error notifications

```

```
