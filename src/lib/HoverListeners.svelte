<script>
  export let width;
  export let height;
  export let xScale;
  export let margin;
  export let hoveredDate;

  const handleMousemove = function (e) {
    hoveredDate = xScale.invert(e.offsetX - margin.left);
  };
</script>

<rect {width} {height} fill="transparent" on:mousemove={handleMousemove} />

<line
  x1={0}
  x2={0}
  y1={0}
  y2={height}
  stroke="black"
  transform="translate({xScale(hoveredDate)} 0)"
  stroke-dasharray="2, 2"
/>
