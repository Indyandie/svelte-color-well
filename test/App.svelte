<script>
  import Color from '../src/components/ColorModal'
  let myColor = 'blue'
</script>

<Color
  bind:color={myColor} 
  type="rgb" 
/>