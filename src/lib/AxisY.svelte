<script>
    export let width;
    export let yScale;
</script>

{#each yScale.ticks(5) as tick}
    <text
        x="0"
        dx="-6"
        y={yScale(tick)}
        text-anchor="end"
        dominant-baseline="middle"
        fill="#999"
    >
        {tick}
    </text>
    <line x1="0" x2={width} y1={yScale(tick)} y2={yScale(tick)} stroke="#999" />
{/each}
