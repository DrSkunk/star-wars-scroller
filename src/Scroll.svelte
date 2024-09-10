<script>
  export let duration = 20;
  // stars in random positions
  const stars = Array(100)
    .fill(null)
    .map(() => ({
      x: Math.random() * 100,
      y: Math.random() * 100,
      opacity: Math.random(),
    }));
</script>

{#each stars as star}
  <div
    class="absolute bg-white rounded-full w-1 h-1"
    style="left: {star.x}vw; top: {star.y}vh; opacity: {star.opacity}"
  />
{/each}
<div
  class="w-screen h-screen flex items-center justify-center whitespace-pre-line text-center"
>
  <div
    style="--duration: {duration}s"
    class="tilt text-white w-3/5 space-y-4 text-5xl min-h-screen"
  >
    <slot />
  </div>
</div>

<style>
  .tilt {
    animation: scroll linear var(--duration) infinite;
  }

  @keyframes scroll {
    from {
      transform: perspective(1000px) rotateX(40deg) translateY(100%);
    }
    to {
      transform: perspective(1000px) rotateX(40deg) translateY(-100%);
    }
  }
</style>
