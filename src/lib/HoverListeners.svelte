<script>
  export let width;
  export let height;
  export let xScale;
  export let margin;
  export let hoveredDate;

  let handleMousemove = function (e) {
    hoveredDate = xScale.invert(e.offsetX - margin.left);
  };

  let handleMouseleave = function () {
    hoveredDate = new Date(xScale.domain()[1]);
  };

  import { timeDay } from "d3-time";
  $: focusableTicks = xScale.ticks(timeDay.every(1));
</script>

<rect
  {width}
  {height}
  fill="transparent"
  on:mousemove={handleMousemove}
  on:mouseleave={handleMouseleave}
/>

<!-- Optional: Add focusable ticks that can be tabbed into by keyboard users -->
{#each focusableTicks as tick}
  <rect
    {height}
    width={width / focusableTicks.length}
    on:focus={() => (hoveredDate = tick)}
    x={xScale(tick)}
    y={0}
    fill="none"
    pointer-events="none"
  />
{/each}

<line
  x1={0}
  x2={0}
  y1={0}
  y2={height}
  stroke="black"
  transform="translate({xScale(hoveredDate)} 0)"
  stroke-dasharray="2, 2"
  pointer-events="none"
/>

<style>
  rect:focus-visible {
    outline: none;
  }
</style>
