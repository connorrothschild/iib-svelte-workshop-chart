<script>
  export let data;
  export let xScale;
  export let yScale;
  export let height;
  export let width;
  export let TRUMP_COLOR;
  export let BIDEN_COLOR;

  export let hoveredIndex;
  import Tooltip from "./Tooltip.svelte";
</script>

<g
  class="hover-listeners"
  on:mouseleave={() => (hoveredIndex = data.Biden.length - 1)}
>
  {#each data.Trump as d, i}
    <rect
      x={xScale(new Date(d.date))}
      y="0"
      width={width / data.Trump.length}
      {height}
      fill="transparent"
      on:mouseover={() => (hoveredIndex = i)}
      on:focus={() => (hoveredIndex = i)}
    />
  {/each}

  <line
    x1={xScale(new Date(data.Trump[hoveredIndex].date))}
    x2={xScale(new Date(data.Trump[hoveredIndex].date))}
    y1={0}
    y2={height}
    stroke="black"
    pointer-events="none"
    stroke-dasharray="2, 2"
  />

  <!-- Tooltips -->
  {#each data.Trump as d, i}
    {#if hoveredIndex == i}
      <Tooltip {d} {xScale} {yScale} color={TRUMP_COLOR} />
    {/if}
  {/each}

  {#each data.Biden as d, i}
    {#if hoveredIndex == i}
      <Tooltip {d} {xScale} {yScale} color={BIDEN_COLOR} />
    {/if}
  {/each}
</g>

<style>
  rect:focus {
    outline: none;
  }

  line {
    transition: x1 500ms ease, x2 500ms ease;
  }
</style>
