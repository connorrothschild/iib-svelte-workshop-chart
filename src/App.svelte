<script>
  import data from "./data/raw.json";

  console.log(data);

  let width = 400;
  let height = 400;

  import { scaleTime, scaleLinear } from "d3-scale";
  import { extent } from "d3-array";

  const margin = { top: 50, right: 50, bottom: 50, left: 50 };
  $: boundedWidth = width - margin.right - margin.left;
  let boundedHeight = height - margin.top - margin.bottom;

  let yScale = scaleLinear().domain([0, 100]).range([boundedHeight, 0]);

  $: xScale = scaleTime()
    .domain(extent(data.Trump, (d) => new Date(d.date)))
    .range([0, boundedWidth]);

  import Line from "./lib/Line.svelte";
  import HoverListeners from "./lib/HoverListeners.svelte";

  const TRUMP_COLOR = "#fa5a50";
  const BIDEN_COLOR = "#5768ac";

  import AxisX from "./lib/AxisX.svelte";
  import AxisY from "./lib/AxisY.svelte";

  let hoveredIndex = data.Biden.length - 1;
</script>

<div class="chart-container" bind:offsetWidth={width}>
  <svg {width} {height}>
    <g class="inner-chart" transform="translate({margin.left} {margin.top})">
      <AxisX {xScale} {boundedHeight} />
      <AxisY {yScale} {boundedWidth} />
      <Line
        data={data.Trump}
        stroke={TRUMP_COLOR}
        {xScale}
        {yScale}
        {hoveredIndex}
      />
      <Line
        data={data.Biden}
        stroke={BIDEN_COLOR}
        {xScale}
        {yScale}
        {hoveredIndex}
      />
      <HoverListeners
        {data}
        {xScale}
        {yScale}
        width={boundedWidth}
        height={boundedHeight}
        {TRUMP_COLOR}
        {BIDEN_COLOR}
        bind:hoveredIndex
      />
    </g>
  </svg>
</div>

<style>
  /* This is where CSS lives */
  svg {
    cursor: crosshair;
  }

  :global(.axis text) {
    fill: #999;
  }

  .chart-container {
    background: #f0f0f0;
  }
</style>
