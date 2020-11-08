<script>
  // import '../styles/modal.less'
  import { createEventDispatcher } from 'svelte'
  import { fade, fly } from 'svelte/transition'
  
  const dispatch = createEventDispatcher()
	const closeModal = () => dispatch('close')
</script>

<section>
  <div class="modal" transition:fly >
    <slot>Modal</slot>
  </div>
</section>

<div 
  class="modal-background" 
  on:click={closeModal}
  transition:fade
/>

<style lang="less">
  @import '../styles/modal.less';

  section {
    position: absolute;
    height: 100%;
    width: 100%;
    display: flex;
    left: 0;
    top: 0;
    justify-content: center;
  }
  
  .modal {
    z-index: 2000;
    margin: auto;
  }

  .modal-background {
    background: white;
    opacity: .6;
    height: 100%;
    width: 100%;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 1999;
  }
</style>