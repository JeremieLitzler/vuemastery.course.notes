# Notes

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

##
