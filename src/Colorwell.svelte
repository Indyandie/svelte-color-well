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
    $: value = 10
    $: valueRange = chrm.hsv(hue, (saturation * 0.01), (1)).hex().toUpperCase()
    $: satRange = chrm.hsv(hue, (1), (value * 0.01)).hex().toUpperCase()
    $: rangeArr = [ valueRange, satRange ]

    $: color = chrm.random()
    
    $: colorContrast = chrm.contrast('white', color) < 4.5 

    function updateColor() {
        color = chrm.hsv(hue, (saturation * 0.01), (value * 0.01)).hex().toUpperCase()
        updateColorGlob()
    }

    function updateColorGlob() {
        colorGlob = color
    }

    function updateColorHSV() {
        let colorHSV = chrm(color).hsv()

        if (hue === NaN) {
            hue = hue
        } else {
            hue = Math.floor(colorHSV[0])   
        }
        saturation = Math.floor(colorHSV[1]*100)
        value = Math.floor(colorHSV[2]*100)
    }

    function updateColorToGlob() {
        color = colorGlob
        updateColorHSV()
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
        updateColorHSV()
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
            <strong class:black={colorContrast} >{color}</strong>
        </div>

        <RangeInput bind:hueColor={rangeArr} hue={true} on:change={updateColor} bind:value={hue} label="Hue" MAX={360}/>
        <RangeInput bind:hueColor={rangeArr} sat={true} on:change={updateColor} bind:value={saturation} label="Saturation" MAX={100}/>
        <RangeInput bind:hueColor={rangeArr} light={true} on:change={updateColor} bind:value={value} label="Value" MAX={100}/>
        
    </div>
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
        color: white;
        border: 2px solid #333;
        cursor: pointer;
    }

    .colorwell-modal {
        width: 320px;
        height: auto;
        padding: 24px;
        border-radius: 16px;
        display: flex;
        flex-direction: column;
        border: 2px solid #aaa; 
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
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 8px;
        font-size: 1.25em; 
        transition: all 200ms ease-out;
        cursor: pointer;
    }

    .colorPal:hover {
        border: 2px solid black;
        transform: scaleY(1.15)
    }

    .black {
        color: black;
    }

    .hidden {
        display: none;
    }

</style>