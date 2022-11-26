<script>
  export let d;
  export let xScale;
  export let yScale;
  export let color;
</script>

<circle
  cx={xScale(new Date(d.date))}
  cy={yScale(d.winprob)}
  r="5"
  fill={color}
/>
<text
  x={xScale(new Date(d.date))}
  y={yScale(d.winprob)}
  dx="8"
  fill={color}
  stroke="white"
  stroke-width="3"
  paint-order="stroke"
  font-weight="600"
  pointer-events="none"
  dominant-baseline="middle"
>
  {Math.round(d.winprob)}
  <tspan dy="1.1em" x={xScale(new Date(d.date))} dx="8">in</tspan>
  <tspan dy="1.1em" x={xScale(new Date(d.date))} dx="8">100</tspan>
</text>
