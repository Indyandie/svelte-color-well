<script>
  import '../styles/color-modal.less'
  import chrm from 'chroma-js'

  import Range from './RangeInput'
  import Well from './Well'
  import Modal from './Modal'

  export let showModal = true

  export let type = 'hsl'
  export let color = '#ff0000'

  $: colorContrast = chrm.contrast('white', color) < 2.3

  // HSL values
  let hslVal = chrm(color).hsl()
  let hueValue = Math.floor(hslVal[0])
  let satValue = Math.floor(hslVal[1]  * 100)
  let lightValue = Math.floor(hslVal[2] * 100)

  // RGB values
  let rgbVal = chrm(color).rgb()
  let redValue = Math.floor(rgbVal[0])
  let greenValue = Math.floor(rgbVal[1])
  let blueValue = Math.floor(rgbVal[2])

  // HSL gradients
  $: hueGradient = () => {
    let grad = 'left,'
    for (let i = 0; i < 405; i += 45) {
      grad += ` hsl(${i}, ${satValue}%, ${lightValue}%)${i < 360 ? ',' : ''}`
    }
    return grad
  }

  $: satGradient = `
    left,
    hsl(${hueValue}, 0%, ${lightValue}%),
    hsl(${hueValue}, 100%, ${lightValue}%)
  `

  $: lightGradient = `
    left,
    hsl(${hueValue}, ${satValue}%, 0%),
    hsl(${hueValue}, ${satValue}%, 50%),
    hsl(${hueValue}, ${satValue}%, 100%)
  `

  // RGB gradients
  $: redGradient = `
    left,
    rgb(0, ${greenValue}, ${blueValue}),
    rgb(255, ${greenValue}, ${blueValue})
  `

  $: greenGradient = `
    left,
    rgb(${redValue}, 0, ${blueValue}),
    rgb(${redValue}, 255, ${blueValue})
  `

  $: blueGradient = `
    left,
    rgb(${redValue}, ${greenValue}, 0),
    rgb(${redValue}, ${greenValue}, 255)
  `

  const updateHslColor = () => {
    color = chrm(`hsl(${hueValue}, ${satValue}%, ${lightValue}%)`).hex()
  }

  const updateRgbColor = () => {
    color = chrm(`rgb(${redValue}, ${greenValue}, ${blueValue})`).hex()
  }

  const updateAllColors = () => {
    hslVal = chrm(color).hsl()
    rgbVal = chrm(color).rgb()
    
    hueValue = Math.floor(hslVal[0])
    satValue = Math.floor(hslVal[1]  * 100)
    lightValue = Math.floor(hslVal[2] * 100)

    redValue = Math.floor(rgbVal[0])
    greenValue = Math.floor(rgbVal[1])
    blueValue = Math.floor(rgbVal[2])
  }
</script>

{#if showModal}
<Modal on:close={() => showModal = false } >
  <Well { color } { colorContrast } />

  {#if type === 'hsl' }
    <Range
    labelName="Hue"
    colorSelFocus={ color }
    bgGrad={ hueGradient() }
    max={ 360 }
    on:change={ updateHslColor }
    bind:value={ hueValue }
  />

  <Range
    labelName="Saturation"
    colorSelFocus={ color }
    bgGrad={ satGradient }
    on:change={ updateHslColor }
    bind:value={ satValue }
  />

  <Range
    labelName="Lightness"
    colorSelFocus={ color }
    bgGrad={ lightGradient }
    on:change={ updateHslColor }
    bind:value={ lightValue }
  />
  {:else if  type === 'rgb' }
  <Range
    labelName="Red"
    colorSelFocus={ color }
    bgGrad={ redGradient }
    max="255"
    on:change={ updateRgbColor }
    bind:value={ redValue }
  />

  <Range
    labelName="Green"
    colorSelFocus={ color }
    bgGrad={ greenGradient }
    max="255"
    on:change={ updateRgbColor }
    bind:value={ greenValue }
  />

  <Range
    labelName="Blue"
    colorSelFocus={ color }
    bgGrad={ blueGradient }
    max="255"
    on:change={ updateRgbColor }
    bind:value={ blueValue }
  />
  {:else}
    None
  {/if}

  <!-- svelte-ignore a11y-no-onchange -->
  <select bind:value={type}  on:change={updateAllColors} >
    <option value="hsl" >HSL</option>
    <option value="rgb" >RGB</option>
  </select>
</Modal>
{/if}

<style>
  :global(
    .modal input[type='range'],
    .modal label
  ) {
    width: 100%;
  }

  :global(.modal) {
    width: 320px;
    margin: 0 auto;
  }

  select {
    height: 44px;
  }

  select {
    display: block;
    font-size: 16px;
    font-family: sans-serif;
    font-weight: 700;
    color: #444;
    line-height: 1.3;
    padding: 8px 16px;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
    margin: 0;
    border: 1px solid #aaa;
    box-shadow: none;
    border-radius: 8px;
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    background: #fff;
  }

  select::-ms-expand {
    display: none;
  }

  select:hover {
    border-color: #888;
  }

  select:focus {
    border-color: #aaa;
    color: #222;
    outline: none;
  }

  select option {
    font-weight: normal;
    font-size: 18px;
    line-height: 2;
  }
</style>