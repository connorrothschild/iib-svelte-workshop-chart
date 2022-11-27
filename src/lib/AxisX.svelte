<script>
  export let height;
  export let xScale;

  const xTicks = xScale.ticks(5);

  import { timeFormat } from "d3-time-format";
  const dateFormat = timeFormat("%b %d");
</script>

<g class='axis x' transform="translate(0 {height})">
  {#each xTicks as tick}
    <line 
      x1={xScale(tick)} 
      x2={xScale(tick)}
      y1='0' 
      y2='6' 
      stroke='#999'
    />
    <text 
      x={xScale(tick)} 
      y='6' 
      dy="3"
      text-anchor='middle'
      dominant-baseline="hanging">
      {dateFormat(tick)}
    </text>
  {/each}
</g>