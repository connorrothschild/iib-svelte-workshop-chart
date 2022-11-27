<script>
  export let width;
  export let yScale;

  const yTicks = yScale.ticks(5);
</script>

<g class='axis y'>
{#each yTicks as tick}
  <text 
    x="0" 
    y={yScale(tick)}
    text-anchor='end'
    dominant-baseline="middle"
    dx="-4"
  >
    {tick}
  </text>
  <line 
    x1="0" 
    x2={width} 
    y1={yScale(tick)} 
    y2={yScale(tick)} 
    stroke='#999' 
    stroke-width="1"
  />
{/each}
</g>