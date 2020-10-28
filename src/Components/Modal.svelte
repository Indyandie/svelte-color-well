<script>
  import '../styles/modal.less'
  import { createEventDispatcher } from 'svelte'
  import { fade, fly } from 'svelte/transition'
  
  const dispatch = createEventDispatcher()
	const closeModal = () => dispatch('close')
</script>

<div class="modal" transition:fly >
  <slot>Modal</slot>
</div>

<div 
  class="modal-background" 
  on:click={closeModal}
  transition:fade
/>

<style>
  .modal {
    z-index: 2000;
    position: relative;
  }

  .modal-background {
    background: white;
    opacity: .6;
    height: 100vh;
    width: 100vw;
    position: absolute;
    left: 0;
    top: 0;
    z-index: 1999;
  }
</style>