<script>
  export let data;
  export let xScale;
  export let yScale;
  export let fill;
  export let hoveredDate;

  $: dataAfterHover = data.filter((d) => new Date(d.date) > hoveredDate);
  $: dataBeforeHover = data.filter((d) => new Date(d.date) <= hoveredDate);

  import { line } from "d3-shape";
  $: lineGenerator = line()
    .x((d) => xScale(new Date(d.date)))
    .y((d) => yScale(d.winprob));
</script>

<path d={lineGenerator(dataAfterHover)} stroke={fill} opacity=".3" />
<path d={lineGenerator(dataBeforeHover)} stroke={fill} />

<style>
  path {
    fill: none;
    stroke-width: 3;
  }
</style>
