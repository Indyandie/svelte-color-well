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


<!-- use the component and bind your color the prop -->
<Colorwell bind:colorGlob={myColor} />

<!-- see it in action -->
<h1>{myColor}</h1>

```


## TODO

* rgb
* fancy input range
* customizations
* spit and polish