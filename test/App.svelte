<script>
  import Range from '../src/components/RangeInput'

  const hueGradient = `left,
    hsl(0, 100%, 50%),
    hsl(45, 100%, 50%),
    hsl(90, 100%, 50%),
    hsl(135, 100%, 50%),
    hsl(180, 100%, 50%),
    hsl(225, 100%, 50%),
    hsl(270, 100%, 50%),
    hsl(315, 100%, 50%),
    hsl(360, 100%, 50%);`

    let defaultVal = 10
    $: currCol = `hsl( ${defaultVal}, 100%, 50%)`
</script>

<h1>Testing {defaultVal}</h1>

<Range/>
<Range 
  colorSel={'var(--track-bg-color)'}
  extraStyles="--thumb-sel-focus: var(--track-bg-color-focus);"
/>
<Range 
  colorSel={'var(--track-bg-color)'}
  extraStyles="--thumb-sel-focus: white;"
/>
<Range 
  extraStyles="--thumb-sel-focus: var(--track-bg-color-focus);"
/>
<Range 
  max={360}
  bind:value={defaultVal}
  bgGrad={hueGradient}
  colorSel={currCol}
/>