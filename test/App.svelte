<script>
  import Color from '../src/components/ColorPicker.svelte'
  let coolColor
</script>

<Color/>

<Color
  color='red'
  type='rgb'
/>

<Color
  bind:color={coolColor}
  type='hsl'
/>

<h1 style='color: white'>{coolColor}</h1>
