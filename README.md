# svelte color well

A color picker.

## Install it

```shell
npm i svelte-color-well
```

## Use it

```html
<script>
  // import it to your component/app
  import ColorWell from 'svelte-color-well'

  // your color
  let yourColor
</script>

<!-- use the component initializes with a random color -->
<ColorWell/>

<!-- initialize color and use rbg sliders -->
<ColorWell
  color='red'
  type='rgb'
/>

<!-- bind color to variable -->
<ColorWell bind:color={yourColor} />

<!-- see it in action -->
<h1>{yourColor}</h1>
```

## TODO

- [ ] text input
