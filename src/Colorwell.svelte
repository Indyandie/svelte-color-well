<script>

    import { onMount, beforeUpdate } from 'svelte';
    import chrm from 'chroma-js'
    import RangeInput from './RangeInput.svelte'

    // Font Awesome
    import Icon from 'svelte-awesome';
    import { eyedropper } from 'svelte-awesome/icons';

    export let colorGlob = chrm.random()
    $: showModal = true

    $: hue = 0
    $: saturation = 100
    $: light = 10

    $: lightRangeCenter     = chrm.hsl(hue, (saturation * 0.01), (.5))
    $: satRangeStart        = chrm.hsl(hue, (0), (light * 0.01))
    $: satRangeEnd          = chrm.hsl(hue, (1), (light * 0.01))
    $: hueRange             = chrm.hsl(hue, 1, 0.5)
    $: rangeArr = {
        ltCen: lightRangeCenter, 
        stRang: [
            satRangeStart, 
            satRangeEnd,
        ], 
        hue: hueRange,
        color: color
    } 
        

    $: color = chrm.random()
    
    $: colorContrast = chrm.contrast('white', color) < 4.5 

    function updateColor() {
        color = chrm.hsl(hue, (saturation * 0.01), (light * 0.01)).hex().toUpperCase()
        updateColorGlob()
    }

    function updateColorGlob() {
        colorGlob = color
    }

    function updateColorHSL() {
        let colorHSL = chrm(color).hsl()

        if (hue === NaN) {
            hue = hue
        } else {
            hue = Math.floor(colorHSL[0])   
        }
        saturation = Math.floor(colorHSL[1]*100)
        light = Math.floor(colorHSL[2]*100)
    }

    function updateColorToGlob() {
        color = colorGlob
        updateColorHSL()
    }


    onMount(async () => {
        if (!colorGlob) {
            updateColorGlob()
        } else {
            updateColorToGlob()
        }
    });
    
    beforeUpdate( async () => {
        if (colorGlob !== color) {
            updateColorToGlob()
        } 
    })

</script>

<div 
    class={`colorwell-selector ${colorContrast ? 'black': '' }`} 
    style={`background: ${color}`} 
    on:click={e => {
        updateColorHSL()
        showModal = !showModal
    }}
>
    <Icon data={eyedropper} scale="1.5" />
</div>

{#if !showModal}
    <div class={`colorwell-modal ${showModal ? 'hidden': ''}`} >

        <div 
            class="colorPal" 
            style={`background: ${color}`}
            on:click="{e => {
                updateColor()
                showModal = true
            }}"
        >
            <strong class:black={colorContrast} >
                <code>{color}</code>
            </strong>
        </div>

        <RangeInput bind:hueColor={rangeArr} hue={true} on:change={updateColor} bind:value={hue} label="Hue" MAX={360}/>
        <RangeInput bind:hueColor={rangeArr} sat={true} on:change={updateColor} bind:value={saturation} label="Saturation" MAX={100}/>
        <RangeInput bind:hueColor={rangeArr} light={true} on:change={updateColor} bind:value={light} label="light" MAX={100}/>
    </div>
    
    <div id="colorwell-overlay" ></div>
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

    #colorwell-overlay {
        background: rgba(255, 255, 255, .5);
        height: 100vh;
        width: 100vw;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 8000;
    }

    .colorwell-modal {
        width: 320px;
        height: auto;
        padding: 24px;
        border-radius: 16px;
        display: flex;
        flex-direction: column;
        border: 2px solid rgb(170, 170, 170, .5); 
        background: white;
        z-index: 90000;
        position: absolute;
        top: 0;
        left: calc(50% - 160px);
    }

    .colorPal {
        padding: 8px 0;
        box-sizing: border-box;
        width: 100%;
        min-height: 32px;
        margin-bottom: 32px;
        color: white;
        border: 2px solid rgb(0, 0, 0, .1);
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 8px;
        font-size: 1.5em; 
        transition: all 200ms ease-out;
        cursor: pointer;
        text-transform: uppercase;
    }

    .colorPal:hover {
        border: 2px solid rgb(0, 0, 0, .25);
        transform: scaleY(1.15)
    }

    .black {
        color: rgb(0, 0, 0, .8);
    }

    .hidden {
        display: none;
    }

</style>