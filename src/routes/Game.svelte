<script lang="ts">
	import Found from './Found.svelte';
	import Grid from './Grid.svelte';
	import { levels } from './level';
	import type { Level } from './level';
	import { shuffle } from './utils';

	const level = levels[0];

	let size: number = level.size;
	let grid: string[] = [];
	let found: string[] = [];

	function create_grid(level: Level) {
		const copy = level.emojis.slice();
		const pairs: string[] = [];
		for (let i = 0; i < level.size ** 2 / 2; i += 1) {
			const index = Math.floor(Math.random() * copy.length);
			const emoji = copy[index];

			copy.splice(index, 1);
			pairs.push(emoji);
		}

		pairs.push(...pairs);

		return shuffle(pairs);
	}
</script>

<div class="game">
	<div class="info">
		<div class="grid-container">
			<Grid
				{grid}
				on:found={(e) => {
					found = [...found, e.detail.emoji];
				}}
				{found}
			/>
		</div>
	</div>
	<div class="info">
		<Found />
	</div>
</div>

<style>
	.game {
		display: flex;
		flex-direction: column;
		justify-content: center;
		height: 100%;
		font-size: min(1vmin, 0.5rem);
	}

	.grid-container {
		width: 80em;
		height: 80em;
		background-color: teal;
	}
	.info {
		width: 80vmin;
		height: 10vmin;
		background-color: purple;
	}
</style>
