<script>
  import '../styles/inputrange.less'
  export let value = 0
  export let id = 'range'
  export let min = 0
  export let max = 100
  export let labelName = 'Label'
  export let colorSel = 'white'
  export let bgGrad
  export let extraStyles = ''
</script>

<label for={id}>
  <strong>{labelName}</strong>
  <code>{value}</code>
</label>

<input
  type="range"
  name="range"
  {max}
  {min}
  {id}
  bind:value
  style="--thumb-sel: {colorSel}; --bg-gradient: {bgGrad}; {extraStyles}"
>