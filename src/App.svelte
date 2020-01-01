<script>
  import { Plyr } from './components/components.module.js';
</script>

<style>
</style>

<h1>Video Player</h1>
<Plyr>
  <video
    crossorigin
    playsinline
    poster="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-HD.jpg"
    src="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-576p.mp4"
  >
    <source
      size="576"
      src="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-576p.mp4"
      type="video/mp4"
    >
    <source
      size="720"
      src="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-720p.mp4"
      type="video/mp4"
    >
    <source
      size="1080"
      src="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-1080p.mp4"
      type="video/mp4"
    >
    <track
      default
      kind="captions"
      label="English"
      src="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-HD.en.vtt"
      srclang="en"
    >
    <track
      kind="captions"
      label="Français"
      src="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-HD.fr.vtt"
      srclang="fr"
    >
    <a
      download=""
      href="https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-576p.mp4"
    >
      Download
    </a>
  </video>
</Plyr>

