<script>
  export let data;
  export let hoveredDate;
  export let xScale;
  export let yScale;
  export let BIDEN_COLOR;
  export let TRUMP_COLOR;

  $: getYValue = (data) =>
    Math.round(data.filter((d) => new Date(d.date) >= hoveredDate)[0]?.winprob);
</script>

<text
  x={xScale(hoveredDate)}
  y={yScale(getYValue(data.Trump))}
  dx="6"
  fill={TRUMP_COLOR}
>
  {getYValue(data.Trump)}
  <tspan dy="1.1em" x={xScale(hoveredDate)} dx="8">in</tspan>
  <tspan dy="1.1em" x={xScale(hoveredDate)} dx="8">100</tspan>
</text>

<text
  x={xScale(hoveredDate)}
  y={yScale(getYValue(data.Biden))}
  dx="6"
  fill={BIDEN_COLOR}
>
  {getYValue(data.Biden)}
  <tspan dy="1.1em" x={xScale(hoveredDate)} dx="8">in</tspan>
  <tspan dy="1.1em" x={xScale(hoveredDate)} dx="8">100</tspan>
</text>

<style>
  text {
    stroke: white;
    stroke-width: 6;
    paint-order: stroke;
    pointer-events: none;
    font-weight: 600;
  }
</style>
