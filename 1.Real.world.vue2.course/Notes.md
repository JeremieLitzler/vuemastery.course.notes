# Notes

[The course is available here](https://www.vuemastery.com/courses/real-world-vue-js).

The project is available on [this repo](https://github.com/JeremieLitzler/vuemastery-projects).

## Vue CLI 3 - Creating our Project

- Install Vue CLI: `npm i -g @vue/cli`
- Create the Project: `vue create project-name`
- Launch the Project: `npm run serve`
- Launch the UI configuration to create, manage or import a project: `vue ui`

## Setup VSC IDE

[See the source guide](https://www.vuemastery.com/blog/vs-code-for-vuejs-developers/).

### What I had

- ESLint
- Prettier _but see below_
- Vue
- Vue VSCode Snippets
- Vetur
- Auto fixe on save in the VSC settings

```json
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
```

### What I didn't have

#### ESLint config

- in `package.json` :

```json
"eslintConfig": {
  "root": true,
  "env": {
    "node": true
  },
  "extends": [
    "plugin:vue/vue3-essential",
    "eslint:recommended"
  ],
  "parserOptions": {
    "parser": "babel-eslint"
  },
  "rules": {}
}
```

- or in `.eslintrc.js`

```js
module.exports = {
  root: true,
  env: {
    node: true,
  },
  extends: ['plugin:vue/vue3-essential', 'eslint:recommended'],
  parserOptions: {
    parser: 'babel-eslint',
  },
  rules: {},
};
```

### Pretty with ESLint

- `npm install --save-dev @vue/eslint-config-prettier`
- `npm install --save-dev prettier eslint-plugin-prettier`
- then add the following to `eslintrc.js`:

```js
...
"extends": [
  "plugin:vue/vue3-essential",
  "@vue/prettier", // ADD
  "eslint:recommended"
],
```

## Vue Router Basics

- The `views` folder is where we store the pages of our website,
- Each page could be made of various components (stored in `components` folder).
- But technically, a view is a component. It is just a high level component.
- The path should start with a `/` otherwise it is treated as a relative route.

### Route naming

A route can be declared by naming them:

```jsx
    <!--by path:-->
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
```

is the same as, by name:

```jsx
    <!--by name:-->
    <div id="nav">
      <router-link :to="{ name: home }">Home</router-link> |
      <router-link :to="{ name: about }">About</router-link>
    </div>
    <router-view />
```

the difference is to allow to change the `path` in only one place, especially in a big app!

### Route renaming

- Using a redirect:

If it happens, and it will, that we need to change the path of a route, we can use a redirect.

```js
  {
    path: "/about-us",//new path
    name: "about",
  }
  ,{
    path: "/about",//old path
    redirect: {name: "about"},
  }
```

- Using an alias is not ideal for SEO.

## Dynamic Routing & History Mode

- To build a dynamic route:

```js
export default new Router({
  routes: [
    ...{
      path: '/user/:username', //<== this is a dynamic route with a dynamic segment
      name: 'user',
      component: User,
    },
  ],
});
```

- To pass on the parameter, use `props: true` on the route and add this to the view:

```html
<script>
  export default {
      props: ['username'];
  };
</script>
```

so that we can use the `username` in the HTML :

```html
<router-link :to="{ name: 'user' }">User: {{username}}</router-link> |
```

### Single File Vue components

## Slots

They are usefull for:

- Display elements: icons, boxes
- Form elements: inputs, select fields, buttons
- Window elements: modals, pop-ups, notifications

If you use multiple slots in a component, using named slots will allow Vue where to put the data from the parent to the child component.

So when you have this:

```html
<template>
  <div>
    <slot></slot>
    <slot></slot>
  </div>
</template>
```

we can update to:

```html
<template>
  <div>
    <slot name="heading"></slot>
    <slot name="paragraph"></slot>
  </div>
</template>
```

and use it like this in the parent:

```html
<MediaBox>
  <h2 slot="heading">Adam Jahr</h2>
  <p slot="paragraph">My words.</p>
</MediaBox>
```

## API Calls with Axios

### Get started with Axios

- Install `json-server` to mock data: `npm i -g json-server`
- Launch the server: `json-server --watch db.json`
- Install axios either via the Vue UI or the NPM CLI

### Make API Calls

We will use the `created` lifecycle hook to load the data from the API using axios get promise.

### Component lifecycle

_When should we call the API?_

In the `created` lifecycle hook. See [the VueJS docs](https://vuejs.org/v2/api/#created).

For the complete documentation,[open this link](https://vuejs.org/v2/guide/instance.html#Instance-Lifecycle-Hooks).

### Creating services

When you call the same API in different place, we need to refractor and create a service so all API calls are made from the same place.

## Managing NPM packages

- what is outdated: `npm outdated`
- update a package: `npm update package-name`
