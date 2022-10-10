<script>
  import { getContext } from "svelte";

  const { styleable } = getContext("sdk");
  const component = getContext("component");
  export let link;
  export let size;
  export let width;

  let getHeight = (size) => {
      switch (true) {
      case link.includes("album"):
          return size ? 360 : 80;
      case link.includes("playlist"):
      case link.includes("artist"):
          return size ? 380 : 80;
      case link.includes("track"):
      case link.includes("show"):
      case link.includes("episode"):
          return size ? 352 : 152;
  }
  }

  $: height = getHeight(size);

  $: src = link.replace(".com/", ".com/embed/");
</script>

<div use:styleable={$component.styles}>
  <iframe
      style="border-radius: 12px;"
      {height}
      {width}
      title="Spotify Embed"
      frameborder="0"
      allowfullscreen
      allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
      loading="lazy"
      {src}
  />
</div>