<script>
    export let height;
    export let xScale;
    export let hoveredDate;
    export let isUnhovered;

    // Format our ticks as short date strings
    import { timeFormat } from "d3-time-format";
    const dateFormat = timeFormat("%b %e");

    const TICK_LENGTH = 8;

    $: ticks = isUnhovered ? xScale.ticks(6) : [hoveredDate];
</script>

{#each ticks as tick}
    <line
        x1={xScale(tick)}
        x2={xScale(tick)}
        y1={height}
        y2={height + TICK_LENGTH}
        stroke="#999"
    />
    <text
        x={xScale(tick)}
        y={height + TICK_LENGTH}
        dy="6"
        dominant-baseline="hanging"
        text-anchor="middle"
        fill="#999"
    >
        {dateFormat(tick)}
    </text>
{/each}

<style>
    text {
        text-transform: uppercase;
        font-size: 0.9rem;
    }
</style>
