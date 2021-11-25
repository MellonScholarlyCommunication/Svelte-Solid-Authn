<script>
	import SolidLogin from "./SolidLogin.svelte";
	import SolidDemo from "./SolidDemo.svelte";

	let webId;
</script>

<main>
	<h1>Hello</h1>
	{#if webId}
	<p>Logged in as {webId}</p>
	{/if}
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	<SolidLogin bind:webId={webId} issuer="https://hochstenbach.inrupt.net"/>
	<SolidDemo/>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
