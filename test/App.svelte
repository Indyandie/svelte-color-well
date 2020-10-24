<script>
  import Color from '../src/ColorWell'
  import Range from '../src/components/RangeInput'
  import Well from '../src/components/Well'
  import Modal from '../src/components/Modal'

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

<Modal>
  <Well/>
  <Range/>
  <Range/>
  <Range/>
</Modal>


<style>
  :global(
    .modal input[type='range'],
    .modal label
  ) {
    width: 100%;
  }
</style>