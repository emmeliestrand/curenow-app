<script>
	import Header from './Header.svelte';
	import Form from './Form.svelte';
	import "@fontsource/montserrat/400.css";
  import "@fontsource/montserrat/600.css";
	import './styles.css';
</script>

<div class="app">
	<Header />
	<main>
		<Form />
		<slot />
		
	</main>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}
	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: flex-end;
		padding: 1rem;
		width: 100%;
		max-width: 375px;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>
