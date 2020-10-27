<script>
  import '../styles/inputrange.less'

  export let value = 0
  export let id = 'range'
  export let min = 0
  export let max = 100
  export let labelName = 'Label'
  export let colorSel = 'white'
  export let colorSelFocus = 'white'
  export let bgGrad
  export let extraStyles = ''
</script>

<label for={id}>
  <strong>{labelName}</strong>
  <code>{value}</code>
</label>

<input
  type="range"
  {max}
  {min}
  {id}
  on:change
  bind:value
  style="--thumb-sel: {colorSel}; --thumb-sel-focus: {colorSelFocus}; --bg-gradient: {bgGrad}; {extraStyles}"
>