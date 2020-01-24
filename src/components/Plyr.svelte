<script>
  import { onMount, onDestroy, createEventDispatcher } from 'svelte';
  import Plyr from 'plyr'
  import '../plyr.scss'

  export let eventsToEmit = []
  export let options = {}
  export let player = {}
  let plyrDiv
  const dispatch = createEventDispatcher();

  $: opts()

  function opts () {
    if (!options.hasOwnProperty('hideYouTubeDOMError')) {
      options.hideYouTubeDOMError = true
    }
    return options
  }

  onMount(async () => {
    player = new Plyr(plyrDiv.firstChild, opts)
    eventsToEmit.forEach(event => dispatchOnPlayerEvent(event))
  })

  onDestroy(() => {
    try {
      player.destroy()
    } catch (e) {
      if (!(opts.hideYouTubeDOMError && e.message === 'The YouTube player is not attached to the DOM.')) {
        // eslint-disable-next-line no-console
        console.error(e)
      }
    }
  })

  function dispatchOnPlayerEvent (event) {
    player.on(event, data => dispatch(event, data.detail.plyr))
  }
</script>

<div bind:this={plyrDiv}>
  <slot></slot>
</div>


