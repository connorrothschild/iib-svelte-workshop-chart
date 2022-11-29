<script>
  import data from "./data/data.json";
  console.log(data);

  const margin = { top: 30, right: 50, bottom: 30, left: 40 };

  let height = 400;
  let width = 400;

  let innerHeight = height - margin.top - margin.bottom;
  $: innerWidth = width - margin.left - margin.right;

  import { scaleLinear, scaleTime } from "d3-scale";
  import Line from "./lib/Line.svelte";

  const yScale = scaleLinear()
    .domain([0, 100]) // INPUT
    .range([innerHeight, 0]); // OUTPUT

  const minDate = new Date(data.Biden[0].date);
  const maxDate = new Date(data.Biden[data.Biden.length - 1].date);

  $: xScale = scaleTime()
    .domain([minDate, maxDate]) // INPUT
    .range([0, innerWidth]); // OUTPUT

  const BIDEN_COLOR = "#5768ac";
  const TRUMP_COLOR = "#fa5a50";

  import AxisX from "./lib/AxisX.svelte";
  import AxisY from "./lib/AxisY.svelte";
  import HoverEvents from "./lib/HoverEvents.svelte";
  import Tooltip from "./lib/Tooltip.svelte";

  let hoveredDate = maxDate;
</script>

<div class="outer">
  <div class="chart-container" bind:clientWidth={width}>
    <h1>How the forecast has changed</h1>
    <svg
      {width}
      {height}
      aria-labelledby="chart-title"
      aria-describedby="chart-description"
      role="img"
    >
      <title id="chart-title">How the forecast has changed</title>
      <desc id="chart-description"
        >A dual line chart showing Donald Trump and Joe Biden's likelihood of
        electoral victory diverging over time. At the final point, on November
        3rd, Biden has an 89 in 100 chance of winning, and Trump has 10 in 100.</desc
      >
      <g transform="translate({margin.left} {margin.top})">
        <AxisX
          height={innerHeight}
          {xScale}
          {hoveredDate}
          isUnhovered={hoveredDate === maxDate}
        />
        <AxisY width={innerWidth} {yScale} />

        <Line
          {xScale}
          {yScale}
          data={data.Biden}
          color={BIDEN_COLOR}
          {hoveredDate}
        />
        <Line
          {xScale}
          {yScale}
          data={data.Trump}
          color={TRUMP_COLOR}
          {hoveredDate}
        />

        <HoverEvents
          width={innerWidth}
          height={innerHeight}
          {xScale}
          {margin}
          {maxDate}
          bind:hoveredDate
        />

        <Tooltip
          {hoveredDate}
          {xScale}
          {yScale}
          data={data.Biden}
          color={BIDEN_COLOR}
        />
        <Tooltip
          {hoveredDate}
          {xScale}
          {yScale}
          data={data.Trump}
          color={TRUMP_COLOR}
        />
      </g>
    </svg>
  </div>
</div>

<style>
  .outer {
    padding: 15px;
    background: #f0f0f0;
    box-shadow: 2px 2px 6px 0 rgba(0, 0, 0, 0.15);
    border-radius: 3px;
  }
  h1 {
    font-size: 28px;
    line-height: 34px;
    color: #222;
    margin-bottom: 10px;
    text-align: center;
    font-weight: 600;
  }
</style>
