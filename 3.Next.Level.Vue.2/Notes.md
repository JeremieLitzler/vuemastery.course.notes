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

## Global and Per-Route guards

## Completing our Progress bar

## Error Handling

## Reusable Form components: BaseInput

## Reusable Form components: BaseButton

## Form Validation with Vuevalidate

## Mixins

## Filters
