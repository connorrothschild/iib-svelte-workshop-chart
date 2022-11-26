<script>
  export let data;
  export let stroke;
  export let xScale;
  export let yScale;
  export let hoveredIndex;

  import { line } from "d3-shape";
  $: lineGen = line()
    .x((d) => xScale(new Date(d.date)))
    .y((d) => yScale(d.winprob));

  $: dataBeforeHover = data.slice(0, hoveredIndex + 1);
  $: dataAfterHover = data.slice(hoveredIndex, data.length - 1);
</script>

<!-- Line after hover -->
<path d={lineGen(dataBeforeHover)} {stroke} opacity="1" />
<path d={lineGen(dataAfterHover)} {stroke} opacity=".35" />

<style>
  path {
    fill: none;
    stroke-width: 4;
  }
</style>
