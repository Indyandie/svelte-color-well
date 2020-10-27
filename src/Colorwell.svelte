<script>
    import chrm from 'chroma-js'
    import Colormodal from './Colormodal.svelte'

    // Font Awesome
    import Icon from 'svelte-awesome';
    import { eyedropper } from 'svelte-awesome/icons'

    export let colorGlob = chrm.random()

    $: hslBox = {
        hue:            Math.floor(chrm(colorGlob).hsl()[0]),
        saturation:     Math.floor(chrm(colorGlob).hsl()[1] * 100),   
        light:          Math.floor(chrm(colorGlob).hsl()[2] * 100),
        contrast:       colorContrast
    }

    $: showModal = true
    $: colorContrast = chrm.contrast('white', colorGlob) < 6 
</script>

<div 
    class={`colorwell-selector ${colorContrast ? 'black': '' }`} 
    style={`background: ${colorGlob}`} 
    on:click={e => {
        showModal = !showModal
    }}
>
    <Icon data={eyedropper} scale="1.5" />
</div>

{#if !showModal}
    <Colormodal
        bind:color={colorGlob}
        bind:showModal={showModal}
        bind:colorContrast={colorContrast}
        bind:hslBox={hslBox}
    />
{/if}

<style>
    .colorwell-selector {
        width: 48px;
        height: 48px;
        border-radius: 100%;
        box-sizing: border-box;
        display: flex;
        justify-content: center;
        align-items: center;
        color: rgba(255, 255, 255, .8);
        border: 2px solid rgb(51, 51, 51, .25);
        cursor: pointer;
    }

    .black {
        color: rgb(0, 0, 0, .8);
    }
</style>