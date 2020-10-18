<script>
    import { onMount, afterUpdate } from 'svelte';
    export let value = 30
    export let MAX = 100
    export let MIN = 0
    export let label = null
    export let hue = false
    export let sat = false
    export let light = false
    export let hueColor

    let lightInput

    function updateGrad() {
        let root = document.documentElement

        let lightGrad = `left, black, ${hueColor.ltCen}, white`
        root.style.setProperty('--light-gradient', lightGrad)

        let satGradient = `left, ${hueColor.stRang[0]}, ${hueColor.stRang[1]}`
        root.style.setProperty('--sat-gradient', satGradient)

        root.style.setProperty('--hue-sel', hueColor.hue)
        root.style.setProperty('--color-sel', hueColor.color)
        
    }

    onMount(async () => {
            updateGrad()
            console.log('alsdfj')
    })

    afterUpdate( async () => {
        updateGrad()
    })

</script>

<label for="range">
    {#if label}
        <strong>{label}</strong>
    {/if}
    <code>{value}</code>
</label>
<input 
    class:hue 
    class:light 
    class:sat 
    on:change
    bind:this={lightInput}
    id="range" 
    type="range"
    bind:value={value}
    min={MIN}
    max={MAX}
>

<style>
    label {
        width: 100%;
        margin-bottom: 8px;
        font-size: 1.5em;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    input {
        margin-bottom: 24px;
    }

    :root {
        --hue-gradient: 
            left,
            hsl(0, 100%, 50%),
            hsl(45, 100%, 50%),
            hsl(90, 100%, 50%),
            hsl(135, 100%, 50%),
            hsl(180, 100%, 50%),
            hsl(225, 100%, 50%),
            hsl(270, 100%, 50%),
            hsl(315, 100%, 50%),
            hsl(360, 100%, 50%);

        --track-bg-color: #333;
        --track-bg-color-focus: cornflowerblue;
        --track-width: 100%;
        --track-width: 100%;
        --track-height: 12px;
        --track-cursor: pointer;
        --track-border-radius: 8px;

        --thumb-border: 10px solid white;
        --thumb-shadow: 0 0 1px 2px  rgba(51, 51, 51, .25);
        --thumb-border-radius: 100%;
        --thumb-size: 32px;
        --thumb-bg: rgba(255, 255, 255, 0);
        --thumb-align: -12px;
    }
/* ++++++++++++++++++++++ */
/* Webkit */
/* ++++++++++++++++++++++ */

    input[type=range] {
        -webkit-appearance: none;
        margin: 16px 0 24px;
        width: 100%;
    }

    input[type=range]:focus {
        outline: none;
    }

    input[type=range]::-webkit-slider-runnable-track {
        width: var(--track-width);
        height: var(--track-height);
        cursor: var(--track-cursor);
        background: var(--track-bg-color);
        border-radius: var(--track-border-radius);
        /* box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d; */
        box-shadow: var(--thumb-shadow);
        /* border: 0.2px solid #010101; */
    }

    input[type=range]:focus::-webkit-slider-runnable-track {
        background: var(--track-bg-color-focus);
    }

    input[type=range]::-webkit-slider-thumb {
        box-shadow: var(--thumb-shadow);
        border: var(--thumb-border);
        height: var(--thumb-size);
        width: var(--thumb-size);
        border-radius: var(--thumb-border-radius);
        background: var(--thumb-bg);
        cursor: var(--track-cursor);
        margin-top: var(--thumb-align);
        -webkit-appearance: none;
    }

    /* Hue Gradient */

    input[type=range].hue::-webkit-slider-runnable-track {
        background-image: -webkit-linear-gradient(var(--hue-gradient));
    }

    input[type=range].hue:focus::-webkit-slider-runnable-track {
        background-image: -webkit-linear-gradient(var(--hue-gradient));
    }

    input[type=range].hue::-webkit-slider-thumb {
        background: var(--hue-sel);
    }

    /* Lightness Gradient */

    input[type=range].light::-webkit-slider-runnable-track {
        background-image: -webkit-linear-gradient(var(--light-gradient));
    }

    input[type=range].light:focus::-webkit-slider-runnable-track {
        background-image: -webkit-linear-gradient(var(--light-gradient));
    }

    input[type=range].light::-webkit-slider-thumb {
        background: var(--color-sel);
    }

    /* Saturation Gradient */

    input[type=range].sat::-webkit-slider-runnable-track {
        background-image: -webkit-linear-gradient(var(--sat-gradient));
    }

    input[type=range].sat:focus::-webkit-slider-runnable-track {
        background-image: -webkit-linear-gradient(var(--sat-gradient));
    }

    input[type=range].sat::-webkit-slider-thumb {
        background: var(--color-sel);
    }

/* ++++++++++++++++++++++ */
/* Firefox */
/* ++++++++++++++++++++++ */

    input[type=range]::-moz-range-track {
        width: var(--track-width);
        height: var(--track-height);
        cursor: var(--track-cursor);
        background: var(--track-bg-color);
        border-radius: var(--track-border-radius);
        box-shadow: var(--thumb-shadow);
    }

    input[type=range]:focus::-moz-range-track {
        background: var(--track-bg-color-focus);
    }

    input[type=range]::-moz-range-thumb {
        box-shadow: var(--thumb-shadow);
        border: var(--thumb-border);
        /* height: var(--thumb-size);
        width: var(--thumb-size); */
        border-radius: var(--thumb-border-radius);
        background: var(--thumb-bg);
        cursor: var(--track-cursor);
        margin-top: var(--thumb-align);
    }

    /* Hue Gradient */

    input[type=range].hue::-moz-range-track {
        background-image: -webkit-linear-gradient(var(--hue-gradient));
    }

    input[type=range].hue:focus::-moz-range-track {
        background-image: -webkit-linear-gradient(var(--hue-gradient));
    }

    input[type=range].hue::-moz-range-thumb {
        background: var(--hue-sel);
    }

    /* Lightness Gradient */

    input[type=range].light::-moz-range-track {
        background-image: -webkit-linear-gradient(var(--light-gradient));
    }

    input[type=range].light:focus::-moz-range-track {
        background-image: -webkit-linear-gradient(var(--light-gradient));
    }

    input[type=range].light::-moz-range-thumb {
        background: var(--color-sel);
    }

    /* Saturation Gradient */

    input[type=range].sat::-moz-range-track {
        background-image: -webkit-linear-gradient(var(--sat-gradient));
    }

    input[type=range].sat:focus::-moz-range-track {
        background-image: -webkit-linear-gradient(var(--sat-gradient));
    }

    input[type=range].sat::-moz-range-thumb {
        background: var(--color-sel);
    }

/* ++++++++++++++++++++++ */
/* Windows */
/* ++++++++++++++++++++++ */

    input[type=range]::-ms-track {
        width: 100%;
        height: 8.4px;
        cursor: pointer;
        background: transparent;
        border-color: transparent;
        border-width: 16px 0;
        color: transparent;
    }

    input[type=range]::-ms-fill-lower {
        background: var(--thumb-bg);
        border: var(--thumb-border);
        border-radius: var(--thumb-border-radius);
    }

    input[type=range]::-ms-fill-upper {
        background: var(--thumb-bg);
        border: var(--thumb-border);
        border-radius: var(--thumb-border-radius);
    }

    input[type=range]:focus::-ms-fill-lower {
        background: var(--thumb-bg);
    }

    input[type=range]:focus::-ms-fill-upper {
        background: var(--thumb-bg);
    }

    input[type=range]::-ms-thumb {
        border: var(--thumb-border);
        height: var(--thumb-size);
        width: var(--thumb-size);
        border-radius: var(--thumb-border-radius);
        background: var(--thumb-bg);
        cursor: var(--track-cursor);
    }

</style>