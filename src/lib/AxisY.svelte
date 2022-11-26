<script>
  export let yScale;
  export let boundedWidth;

  let yTicks = yScale.ticks(5);
</script>

<g class="axis y">
  {#each yTicks as tick}
    <text
      y={yScale(tick)}
      x={0}
      dx="-6"
      dominant-baseline="middle"
      text-anchor="end">{tick}</text
    >
    <line
      x1={0}
      x2={boundedWidth}
      y1={yScale(tick)}
      y2={yScale(tick)}
      stroke="#999"
    />
  {/each}
</g>
