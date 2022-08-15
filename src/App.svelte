<script>
  import { onMount } from 'svelte';
  import * as NGL from 'ngl';

  let structure = "7QO7";

  onMount(async () => {

    // Create NGL Stage object
    let stage = new NGL.Stage( "protein" );

    stage.setParameters({
      backgroundColor: "white"
    });

    window.addEventListener( "resize", function( event ){
      stage.handleResize();
    }, false );

    // Load PDB entry 
    stage.loadFile( `rcsb://${structure}`).then(o => {
      o.addRepresentation("cartoon", { color: "bfactor" })
      o.autoView()
    });
    

	});

</script>

<p>Showing structure: {structure}</p>
<div id="protein"></div>
<input bind:value={structure}>
<style>

  p {
    text-align: center;
    font-family: 'Courier New', Courier, monospace;
  }

  #protein {
    aspect-ratio: 1 / 1;
    height: 50vh;
    margin: 0 auto;
    border: 3px solid black;
  }

</style>
