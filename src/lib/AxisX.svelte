<script>
  export let boundedHeight;
  export let xScale;

  let xTicks = xScale.ticks(5);

  const TICK_LENGTH = 10;

  import { timeFormat } from "d3-time-format";
  const dateFormat = timeFormat("%b %d");
</script>

<g class="axis x">
  {#each xTicks as tick}
    <line
      x1={xScale(tick)}
      x2={xScale(tick)}
      y1={boundedHeight}
      y2={boundedHeight + TICK_LENGTH}
      stroke="#999"
    />
    <text
      x={xScale(tick)}
      y={boundedHeight + TICK_LENGTH}
      dy="8"
      dominant-baseline="hanging"
      text-anchor="middle">{dateFormat(tick)}</text
    >
  {/each}
</g>
