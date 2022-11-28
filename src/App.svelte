<script>
  import data from "./data/data.json";
  console.log(data);

  let width = 400;
  const height = 400;

  const margin = { top: 30, right: 50, bottom: 35, left: 50 };

  $: innerWidth = width - margin.right - margin.left;
  const innerHeight = height - margin.top - margin.bottom;

  import { scaleTime, scaleLinear } from "d3-scale";
  const yScale = scaleLinear().domain([0, 100]).range([innerHeight, 0]);

  import { extent } from "d3-array";
  $: xScale = scaleTime()
    .domain(extent(data.Trump.map((d) => new Date(d.date))))
    .range([0, innerWidth]);

  import Line from "./lib/Line.svelte";

  const BIDEN_COLOR = "#5768ac";
  const TRUMP_COLOR = "#fa5a50";

  import AxisX from "./lib/AxisX.svelte";
  import AxisY from "./lib/AxisY.svelte";
  import Tooltip from "./lib/Tooltip.svelte";
  import HoverListeners from "./lib/HoverListeners.svelte";

  let hoveredDate = new Date(data.Trump[data.Trump.length - 1].date);
</script>

<!-- FIXME: Add aria-labelledby, title, etc. -->
<div class="chart-container" bind:clientWidth={width}>
  <svg {width} {height}>
    <g class="inner-chart" transform="translate({margin.left}, {margin.top})">
      <!-- Axes -->
      <AxisX height={innerHeight} {xScale} {hoveredDate} />
      <AxisY width={innerWidth} {yScale} />

      <!-- Lines -->
      <Line
        data={data.Trump}
        {xScale}
        {yScale}
        fill={TRUMP_COLOR}
        {hoveredDate}
      />
      <Line
        data={data.Biden}
        {xScale}
        {yScale}
        fill={BIDEN_COLOR}
        {hoveredDate}
      />

      <!-- Hover Listeners -->
      <HoverListeners
        width={innerWidth}
        height={innerHeight}
        {xScale}
        {margin}
        bind:hoveredDate
      />

      <!-- Tooltip -->
      <Tooltip
        {data}
        {hoveredDate}
        {xScale}
        {yScale}
        {BIDEN_COLOR}
        {TRUMP_COLOR}
      />
    </g>
  </svg>
</div>

<style>
  :global(.axis text) {
    fill: #999;
    font-size: 0.8rem;
  }

  .chart-container {
    background: rgb(240, 240, 240);
  }

  svg {
    cursor: crosshair;
  }
</style>
