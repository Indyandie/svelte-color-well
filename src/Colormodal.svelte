<script>
    import { onMount, beforeUpdate } from 'svelte'

    import chrm from 'chroma-js'
    import RangeInput from './RangeInput.svelte'

    export let color
    export let showModal
    export let colorContrast
    export let hslBox

    $: lightRangeCenter     = chrm.hsl(hslBox.hue, (hslBox.saturation * 0.01), (.5))
    $: satRangeStart        = chrm.hsl(hslBox.hue, (0), (hslBox.light * 0.01))
    $: satRangeEnd          = chrm.hsl(hslBox.hue, (1), (hslBox.light * 0.01))
    $: hueRange             = chrm.hsl(hslBox.hue, 1, 0.5)
    $: rangeArr = {
        ltCen: lightRangeCenter, 
        stRang: [
            satRangeStart, 
            satRangeEnd,
        ], 
        hue: hueRange,
        color: color
    }


    function updateColor() {
        color = chrm.hsl(hslBox.hue, (hslBox.saturation * 0.01), (hslBox.light * 0.01)).hex()
    }


    function updateColorHSL() {
        let colorHSL = chrm(color).hsl()

        if (hslBox.hue === NaN) {
            hslBox.hue = hslBox.hue
        } else {
            hslBox.hue = Math.floor(colorHSL[0])   
        }
        hslBox.saturation = Math.floor(colorHSL[1]*100)
        hslBox.light = Math.floor(colorHSL[2]*100)
    }

    onMount(async () => {
        updateColorHSL()
    })
    
    beforeUpdate( async () => {
        updateColor()
    }) 

</script>

<div class="colorwell-overlay" >
    <div class={`colorwell-modal ${showModal ? 'hidden': ''}`} >

        <div 
            class="colorPal" 
            style={`background: ${color}`}
            on:click={e => {
                showModal = true
            }}
        >
            <strong class:black={colorContrast} >
                <code>{color.toUpperCase()}</code>
            </strong>
        </div>

        <RangeInput bind:hueColor={rangeArr} on:change={updateColor} hue={true}  bind:value={hslBox.hue} label="Hue" MAX={360}/>
        <RangeInput bind:hueColor={rangeArr} on:change={updateColor} sat={true}  bind:value={hslBox.saturation} label="Saturation" MAX={100}/>
        <RangeInput bind:hueColor={rangeArr} on:change={updateColor} light={true}  bind:value={hslBox.light} label="Lightness" MAX={100}/>
    </div>
</div>


<style>

    .colorwell-overlay {
        background: rgba(255, 255, 255, .5);
        height: 100vh;
        width: 100vw;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 8000;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow-y: scroll;
        backdrop-filter: blur(5px);
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
        flex-shrink: 0;
        /* margin-bottom: auto; */
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
        font-size: 1.75em; 
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

    /* Small Devices, Phones */ 
    @media only screen and (max-width : 620px) {

        .colorwell-modal {
            width: 100%;
            height: auto;
            box-sizing: border-box;
            padding: 0 12px 24px;
            border-radius: 0;
            margin-bottom: 0;
            margin-top: auto;
            border: 0;
        }

        .colorwell-overlay {
            background: rgba(255, 255, 255, .7);
            border: 2px solid rgb(170, 170, 170, .25); 
            border: 0;
            position: absolute;
            position: fixed;
            bottom: 0;
            height: 100vh;
        }

        .colorPal {
            margin-bottom: 16px;
            width: 100vw;
            position: sticky;
            top: 0;
            margin-left: -12px;
            border-radius: 0;
            padding: 24px 0;
        }

    }

</style>