<script>

    import { onMount } from 'svelte';
    import chrm from 'chroma-js'
    import RangeInput from './RangeInput.svelte'

    // Font Awesome
    import Icon from 'svelte-awesome';
    import { tint } from 'svelte-awesome/icons';

    export let colorGlob = color

    $: hue = Math.floor(Math.random() * 360)
    $: saturation = Math.floor(Math.random() * 100)
    $: value = Math.floor(Math.random() * 100)
    $: color = chrm.hsv(hue, (saturation * 0.01), (value * 0.01)).hex().toUpperCase()
    $: colorContrast = chrm.contrast('white', color) < 4.5 
    $: showModal = true

    function updateColor() {
        colorGlob = color
    }

    onMount(async () => {
		colorGlob = color
	});

</script>

<h1>{colorGlob}</h1>

<div 
    on:load={updateColor}
    class={`color-selector ${colorContrast ? 'black': '' }`} 
    style={`background: ${color}`} 
    on:click={e => showModal = false }
>
    <Icon data={tint} scale="2" />
</div>

<div class={`modal ${showModal ? 'hidden': ''}`} >

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

    <RangeInput bind:value={hue} label="Hue" MAX={360}/>
    <RangeInput bind:value={saturation} label="Saturation" MAX={100}/>
    <RangeInput bind:value={value} label="Value" MAX={100}/>
    
</div>


<style>

    .color-selector {
        width: 48px;
        height: 48px;
        border-radius: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
        cursor: pointer;
    }

    .modal {
        width: 320px;
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
        transition: all 300ms ease-in;
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