<script>
	import IconButton from './../../shared/component/button/IconButton.svelte';
	import TopMenu from './TopMenu.svelte';
</script>
<div class="TopMenu">
	<IconButton icon="flag">
		QUICK START
	</IconButton>
	<IconButton onClick={()=>window.open("https://github.com/tncrazvan/CatPaw")} icon="archive">
		REPOSITORY
	</IconButton>
</div>

<style>
	.TopMenu{
		padding: 1rem;
		border-bottom: 1px solid var(--main-horizontalLine-color);
	}
</style>