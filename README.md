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
    import Colorwell from 'svelte-color-well'

    // your color var
    let myColor
</script>

<!-- use the component initializes with a random color -->
<Colorwell/>

<!-- initialize color and use rbg -->
<Colorwell
  bind:myColor={myColor}
  type='rgb'
/>

<!-- see it in action -->
<h1>{myColor}</h1>
```

## TODO

- [ ] text input
