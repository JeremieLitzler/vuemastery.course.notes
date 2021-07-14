# Next-Level Vue 2

## Progress bar: axios interceptors

The goal is to implement a mean to let the user know that data is loading.

The course uses [NProgress](https://ricostacruz.com/nprogress/).

Using `json-server`, we can slow down the api call with `-d` option.

`json-server -d 1500 db.json`

However, there are 2 issues :

1/ this is not optimal for multiple api calls.

The solution is to start the progress bar on the first call and end it on the last api call to load the view.

For that we will use a Vuex module.

2/ the view template is loaded before the data. We don't want that.

### Other usages of interceptors

- On request, set authorization tokens
- On response, format or filter the date before it reaches into your app.
- On response, catch your api errors.

## In-component Route guards

Vue provides lifecycle hook methods:

- `beforeCreate()`
- `created()`
- `beforeMount()`
- `mounted()`
- `beforeUpdate()`
- `updated()`
- `beforeDetroy()`
- `detroyed()`

With Vue router, we add 3 more methods, called _Route Navigation Guards_:

- `beforeRouteEnter(routeTo, routeFrom, next)`
  - called before `created`, so no access to `this` in the component.
- `beforeRouteUpdate(routeTo, routeFrom, next)`
- `beforeRouteLeave(routeTo, routeFrom, next)`

- `routeTo` is the route we are going to.
- `routeFrom` is the route we are coming from.
- `next` is a function that must be called to the resolve the hook.

See [docs](https://router.vuejs.org/guide/advanced/navigation-guards.html#in-component-guards).

## Global and Per-Route guards

It can help us remove the use of the state in the components.

We can use two guards:

```js
//run before navigating to the component
router.beforeEach((to, from, next) => {
  next();
});

//run right before the component is created (but after beforeRouteEnter?)
router.afterEach((to, from) => {
  console.log(to, from);
});
```

We set them the router file.

The per-route guard is `beforeEnter` set on the route object.

- it runs after `beforeEach` and before `beforeRouteEnter`

## Completing our Progress bar

## Error Handling

## Reusable Form components: BaseInput

## Reusable Form components: BaseButton

## Form Validation with Vuevalidate

## Mixins

## Filters
