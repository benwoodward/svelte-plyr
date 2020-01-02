<script>
  import { onMount, onDestroy } from 'svelte';
  import Plyr from 'plyr'

  export let emit = []
  export let options = {}
  export let player = {}
  let plyrDiv

  $: opts()

  function opts () {
    if (!options.hasOwnProperty('hideYouTubeDOMError')) {
      options.hideYouTubeDOMError = true
    }
    return options
  }

  onMount(async () => {
    player = new Plyr(plyrDiv.firstChild, opts)
    /* emit.forEach(element => { */
    /*   player.on(element, plyrDiv.emitPlayerEvent) */
    /* }) */
  })

  /* onDestroy(() => { */
  /*   try { */
  /*     this.player.destroy() */
  /*   } catch (e) { */
  /*     if (!(this.opts.hideYouTubeDOMError && e.message === 'The YouTube player is not attached to the DOM.')) { */
  /*       // eslint-disable-next-line no-console */
  /*       console.error(e) */
  /*     } */
  /*   } */
  /* }) */

  /* function emitPlayerEvent (event) { */
  /*   this.$emit(event.type, event) */
  /* } */
</script>

<style lang="css" src="../../node_modules/plyr/dist/plyr.css" global>
</style>

<div bind:this={plyrDiv}>
  <slot></slot>
</div>


