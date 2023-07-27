<script>
	import ProgressBar from '../components/ProgressBar.svelte';
	import logo from '$lib/images/curenow.svg';
	import Icon from '@iconify/svelte';
</script>

<header>
	<div class="header-content">
		<div class="back-arrow">
			<Icon icon="material-symbols:arrow-circle-left-outline-rounded" width="2rem" />
		</div>
		<h1>Heartburn checker</h1>
		<div>
			<img src={logo} alt="Curenow" />
		</div>
	</div>
	<ProgressBar />
</header>

<style>
	header {
		background-color: var(--blue-600);
		padding: var(--grid-base);
	}
	.header-content{
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.back-arrow {
		color: var(--white-100);
	}
</style>
