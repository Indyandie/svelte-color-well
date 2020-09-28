<script>
    import Colorwell from '../src/Colorwell'
    import chrm from 'chroma-js'

    let myColor = '#FF0000'

    function randBaseColor() {
        myColor = chrm.random()
    }

    document.addEventListener('keydown', event => {
        if (event.code === 'Space') {
            randBaseColor()
        }
    })

</script>

<h1>{myColor}</h1>
<input type="text" bind:value={myColor}>

<Colorwell bind:colorGlob={myColor} />
<Colorwell />