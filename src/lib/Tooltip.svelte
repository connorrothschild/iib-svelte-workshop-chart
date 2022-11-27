<script>
  export let data;
  export let hoveredDate;
  export let xScale;
  export let yScale;
  export let BIDEN_COLOR;
  export let TRUMP_COLOR;

  $: getYValue = data =>
    Math.round(data.filter(d => new Date(d.date) >= hoveredDate)[0]?.winprob);
</script>

<text
  x={xScale(hoveredDate)}
  y={yScale(getYValue(data.Trump))}
  dx="6"
  fill={TRUMP_COLOR}
>
{getYValue(data.Trump)} in 100
</text>

<text
  x={xScale(hoveredDate)}
  y={yScale(getYValue(data.Biden))}
  dx="6"
  fill={BIDEN_COLOR}
>
{getYValue(data.Biden)} in 100
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