# Svelte Colorwell
A color picker.


## Install it
```shell
npm i svelte-color-well
```

## Using it
```html
<script>
    // import it to your component/app
    import Colorwell from 'svelte-color-well'

    // your color var
    let myColor
</script>

<!-- use the component initializes with a random color -->
<Colorwell/>

<!-- use the component and initialize color -->
<Colorwell bind:colorGlob={myColor} />

<!-- see it in action -->
<h1>{myColor}</h1>
```

## TODO

* rgb
* fancy input range
* customizations
* spit and polish