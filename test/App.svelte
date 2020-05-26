<script>
    import Colorwell from '../src/Colorwell'
    $: myColor = '#FF0000'
</script>

<h1>{myColor}</h1>
<input type="text" bind:value={myColor}>

<Colorwell bind:colorGlob={myColor} />