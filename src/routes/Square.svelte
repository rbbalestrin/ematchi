<script lang="ts">
	export let emoji: string;
	export let selected: boolean;
	export let found: boolean;
</script>

<div class="square" class:flipped={selected}>
	<button on:click />
	{#if !found}
		<span>{emoji}</span>
	{/if}
</div>

<style>
	.square {
		display: flex;
		justify-content: center;
		align-content: center;
		background-color: red;
	}

	.flipped button {
		background-color: red;
	}
	button {
		position: absolute;
		width: 100%;
		height: 100%;
	}
	span {
		font-size: 5em;
		pointer-events: none;
	}
</style>
