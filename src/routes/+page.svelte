<script lang="ts">
	import { GUI, guiControls } from '$lib/gui'
	import * as d3 from 'd3';

	const gui = guiControls({
		x: 120,
		y: 120,
		radius: 80,
		color: '#17191c',
		stroke: '#00ffcc',
		size: 4,
		dash: { value: 0, min: 0, max: 1.1, step: 0.01 },
		offset: { value: 0, min: 0, max: 1.1, step: 0.01 },
		spacing: { value: 3, min: 0, max: 10, step: 0.1}
	})

	const sizeX = 3; // Number of circles in the X direction
	const sizeY = 3; // Number of circles in the Y direction
	const startingX = 50;
	const startingY = 50;
	let positions = [];

	for (let i = 0; i < sizeX; i++) {
		for (let j = 0; j < sizeY; j++) {
			positions.push({
				x: startingX + i * ($gui.spacing.value + $gui.radius * 3),
				y: startingY + j * ($gui.spacing.value + $gui.radius * 3)
			});
		}
	}
</script>

<GUI controls={gui} />

<svg width="800" height="800" viewBox="0 0 800 800">
	{#each positions as pos, index}
		<g transform="translate({pos.x - $gui.radius}, {pos.y - $gui.radius})">
			<circle
				cx={$gui.x}
				cy={$gui.y}
				r={$gui.radius}
				fill={$gui.color}
				stroke={$gui.stroke}
				stroke-width={$gui.size}
				stroke-dasharray={$gui.dash.value}
				stroke-dashoffset={$gui.offset.value}
				pathLength="1"
			/>
		</g>
	{/each}
</svg>
