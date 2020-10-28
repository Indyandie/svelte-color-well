<script>
  import Color from '../src/components/ColorModal'
  let myColor = 'blue'
  
  let closeModal = false
</script>

<button on:click={() => closeModal = true } >showModal</button>

<Color
  bind:color={myColor} 
  type="rgb" 
  bind:showModal={closeModal}
/>