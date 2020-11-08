<script>
  // import '../styles/well.less'

  export let color = '#2DB7F2'
  export let colorContrast = false
</script>

<div
  class="colorPal"
  style={ `background: ${color}` }
>
  <strong class:black={colorContrast} >
    <code>{ color.toUpperCase() }</code>
  </strong>
</div>

<style lang="less">
  @import '../styles/well.less';

  .black {
    color: black;
  }
</style>