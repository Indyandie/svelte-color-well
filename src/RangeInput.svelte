<script>
    export let value = 30
    export let MAX = 100
    export let label = null
</script>

<label for="range">
    {#if label}
        <strong>{label}</strong>
    {/if}
    {value}</label>
<input on:change id="range" type="range" bind:value={value} max={MAX}>

<style>
    label {
        width: 100%;
        margin-bottom: 8px;
        font-size: 1.5em;
        display: flex;
        justify-content: space-between;
    }

    input {
        margin-bottom: 24px;
    }
</style>