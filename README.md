[![Known Vulnerabilities](https://snyk.io/test/github/benwoodward/svelte-plyr/badge.svg)](https://snyk.io/test/github/benwoodward/svelte-plyr)
[![install size](https://badgen.net/packagephobia/install/svelte-plyr)](https://packagephobia.now.sh/result?p=svelte-plyr)
[![npm package version](https://badgen.net/npm/v/svelte-plyr)](https://npm.im/svelte-plyr)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

# svelte-plyr

## A Svelte 3 component-wrapper for [Plyr.js](https://plyr.io)

This component is released under a MIT license.

Examples: [https://github.com/benwoodward/svelte-plyr/blob/master/src/App.svelte](App.svelte)

## Installation

Install the plugin + required dependencies:

```bash
npm install --save svelte-plyr plyr rollup-plugin-postcss node-sass
```

Add `postcss` to your `rollup.config.js` (or `webpack.config.js`)

```javascript
import postcss from 'rollup-plugin-postcss';

export default {
	input: 'src/main.js',
	output: {
		sourcemap: true,
		format: 'iife',
		name: 'app',
		file: 'public/build/bundle.js'
	},
	plugins: [
    postcss(),
  ]
};
```

You may then begin to write a parent component that leverages the `<Plyr>` component:

`components/YoutubePlyr.svelte`

```html
<script>
  import { Plyr } from "svelte-plyr";
  export let videoId;

  function logEvent(event) {
    console.log(event)
  }

  let player
</script>

<div class="youtube-plyr">
  <button on:click={() => player.play()}>PLAY</button>
  <button on:click={() => player.pause()}>PAUSE</button>
  <Plyr on:timeupdate={logEvent} bind:player={player}>
    <div class="plyr__video-embed">
      <iframe
        src="https://www.youtube.com/embed/{videoId}?iv_load_policy=3&modestbranding=1&playsinline=1&showinfo=0&rel=0&enablejsapi=1"
        allowfullscreen allowtransparency allow="autoplay">
      </iframe>
    </div>
  </Plyr>
</div>

<style>
.youtube-plyr {
  max-width: 800px;
}
</style>
```

## Props

The `<Plyr>` component is equipped with [all of Plyr's options](https://github.com/sampotts/plyr#options)! Just pass them in as props. Example:

```html
<Plyr autoplay=true muted=false />
```

## Events

The `<Plyr />` component can be configured to emit specified events. In this example, the `logEvent` function is called whenever the `plyr.js` emits the [timeupdate](https://github.com/sampotts/plyr#standard-media-events) `logEvent` event.

```html
<script>
  import { Plyr } from "svelte-plyr";

  function logEvent(event) {
    console.log(event)
  }

  let player
  let eventsToEmit = ['timeupdate']
</script>

<Plyr on:timeupdate={logEvent} eventsToEmit={eventsToEmit} bind:player={player}>
  // video embed code omitted
</Plyr>
```

