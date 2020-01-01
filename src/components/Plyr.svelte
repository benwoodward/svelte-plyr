<script>
  import { onMount, onDestroy } from 'svelte';
  import Plyr from 'plyr'

  export let emit = []
  export let options = {}
  export let player = {}
  export let plyr

  $: opts()

  function opts () {
    if (!options.hasOwnProperty('hideYouTubeDOMError')) {
      options.hideYouTubeDOMError = true
    }
    return options
  }

  onMount(async () => {
    player = new Plyr(plyr.firstChild, this.opts)
    emit.forEach(element => {
      player.on(element, this.emitPlayerEvent)
    })
  })

  onDestroy(() => {
    try {
      this.player.destroy()
    } catch (e) {
      if (!(this.opts.hideYouTubeDOMError && e.message === 'The YouTube player is not attached to the DOM.')) {
        // eslint-disable-next-line no-console
        console.error(e)
      }
    }
  })

  function emitPlayerEvent (event) {
    this.$emit(event.type, event)
  }
</script>

<div bind:this={plyr}>
  <slot></slot>
</div>

<style src="../../node_modules/plyr/dist/plyr.css">
</style>

