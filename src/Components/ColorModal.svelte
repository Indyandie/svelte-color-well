<script>
import '../styles/color-modal.less'
import Range from './RangeInput'
import Well from './Well'
import Modal from './Modal'

$: color = `hsl(${hueValue}, ${satValue}%, ${lightValue}%)`

let hueValue = 30
$: hueGradient = () => {
  let grad = 'left,'
  for (let i = 0; i < 405; i += 45) {
    grad += ` hsl(${i}, ${satValue}%, ${lightValue}%)${i < 360 ? ',' : ''}`
  }
  return grad
}

let satValue = 50
$: satGradient = `
  left,
  hsl(${hueValue}, 0%, ${lightValue}%),
  hsl(${hueValue}, 100%, ${lightValue}%)
`

let lightValue = 75
$: lightGradient = `
  left,
  hsl(${hueValue}, ${satValue}%, 0%),
  hsl(${hueValue}, ${satValue}%, 50%),
  hsl(${hueValue}, ${satValue}%, 100%)
`

</script>

<Modal>
  <Well { color } />

  <Range
    labelName="Hue"
    colorSel={`hsl(${hueValue}, ${satValue}%, ${lightValue}%)`}
    bgGrad={hueGradient()}
    max={360}
    bind:value={hueValue}
  />
  <Range
    labelName="Saturation"
    colorSel={`hsl(${hueValue}, ${satValue}%, ${lightValue}%)`}
    bgGrad={satGradient}
    bind:value={satValue}
  />
  <Range
    labelName="Lightness"
    colorSel={`hsl(${hueValue}, ${satValue}%, ${lightValue}%)`}
    bgGrad={lightGradient}
    bind:value={lightValue}
  />
</Modal>


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
</style>