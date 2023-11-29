<script>
	import { createEventDispatcher, onMount } from "svelte";

	/**
	  * Parent components can use bind:dialog to get a
	  * reference so they can call show(), showModal(), and close().
	  */
	  export let dialog;

	/**
	 * Footer Buttons
     * @type {any[]}
     */
	 export let footerButtons = [];

	// headerText text to display in the dialog header.
	export let headerText = "";

	const dispatch = createEventDispatcher();

	/**
     * @param {any} e
     */
	function buttonHandler(e) {
		console.log(e);
		dispatch("footerButtonHandler", e);
	}
</script>

<svelte:window
	on:keydown={(e) => {
		/*
		  Dispatch event on escape key
	  	*/
		if (e.code === "Escape") {
			e.preventDefault(); //prevents default dialog escape
			dispatch("escapePressed");
		}
	}}
/>
<dialog class="dialogContainer" bind:this={dialog}>
	<header>
		<h1>{headerText}</h1>
	</header>
	<main>
		<slot />
	</main>
	<footer>
		{#each footerButtons as button}
			<button on:click={buttonHandler(button)}>{button.label}</button>
		{/each}
	</footer>
</dialog>

<style>

	.dialogContainer {
		padding: 48px;
		margin: auto;
		background-color: var(--dialogContainerBackgroundColor, #FFF);
		border-radius: 8px;
		display: flex;
		flex-direction: column;
		gap: 28px;
		box-shadow: 0px 4px 44px 0px rgba(0, 73, 125, 0.05);
		border: none;
	}

	header {
		display: flex;
		flex-direction: row;
		gap: 28px;
		justify-content: space-between;
		align-items: center;
		box-sizing: border-box;
		color: var(--dialogHeaderColor, #222);
		font-weight: bold;
		width: 100%;
		margin: 0px;
		padding: 0px;
	}
	 header h1 {
		width: 100%;
		margin: 0px;
		padding: 0px;
	 }

	main {
		font-family: Roboto Light, Roboto, RobotoBlack, system-ui, -apple-system, BlinkMacSystemFont, 'Helvetica Neue', sans-serif;
		font-size: 14px;
		font-weight: light;
	}

	footer {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}

	footer button:first-of-type {
		background-color: var(--dialogFooterFirstButtonBackgroundColor, #0094FF);
		border: 0px; /* Accent primary */
		border-radius: 4px;
		color: var(--dialogFooterFirstButtonColor, #FFF);
	}

	footer button:first-of-type:hover {
		background-color: var(--dialogFooterFirstButtonHoverBackgroundColor, #0094FF);
		filter: brightness(0.9);
	}
	
	button {
		background-color: transparent;
		box-sizing: border-box;
		border: var(--dialogFooterButtonBorder, 1px solid #0094FF); /* Accent primary */
		border-radius: 4px;
		color: var(--dialogFooterButtonColor, #0094FF); 
		padding-left: 20px;
		padding-top: 12px;
		padding-right: 20px;
		padding-bottom: 12px;
	}

	button:hover {
		border: var(--dialogFooterButtonHoverBorder, 3px solid #0094FF); 
		box-sizing: border-box;
	}

	dialog::backdrop,
	:global(dialog + .backdrop) {
		/* This is a transparent shade of gray. */
		/* Why is this ignored in Safari? */
		background: rgba(236, 237, 241, 0.70);
		backdrop-filter: blur(5px);
	}
</style>
