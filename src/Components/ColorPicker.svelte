<script>
  // import '../styles/color-picker.less'

  // Font Awesome
  import Icon from 'svelte-awesome';
  import { eyedropper } from 'svelte-awesome/icons'
  import { contrast, random } from 'chroma-js'

  import Modal from './ColorModal.svelte'
  
  export let color = random().hex()
  export let type = 'hsl'

  $: pickerContrast = contrast('white', color) < 2.3
  let closeModal = false
</script>

<div 
  class={`colorwell-selector${pickerContrast ? ' black' : ''}`} 
  style={`background: ${color}`} 
  on:click={() => closeModal = true }
>
  <Icon data={eyedropper} scale="1.5" />
</div>

<Modal
  bind:color={color} 
  bind:showModal={closeModal}
  bind:type={type}
/>

<style lang="less" >
  @import '../styles/color-picker.less';

  .colorwell-selector {
      width: 48px;
      height: 48px;
      border-radius: 100%;
      box-sizing: border-box;
      display: flex;
      justify-content: center;
      align-items: center;
      color: rgba(255, 255, 255, .8);
      border: 2px solid rgb(51, 51, 51, .25);
      cursor: pointer;
  }

  .black {
      color: rgb(0, 0, 0, .8);
  }
</style>