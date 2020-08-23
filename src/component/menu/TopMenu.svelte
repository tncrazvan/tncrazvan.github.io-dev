<script>
	import IconButton from '../button/IconButton.svelte';
	import TopMenu from './TopMenu.svelte';
	import { navigate } from 'svelte-routing';
</script>
<div class="TopMenu">
	<div class="row" style="margin-bottom:0">
		<div class="
			col
			offset-s0 s12
			offset-m0 m12
			offset-l1 l10
			offset-xl2 xl8
		">
			<IconButton icon="flag" onClick={()=>navigate("/")}>
				QUICK START
			</IconButton>
			<IconButton onClick={()=>window.open("https://github.com/tncrazvan/catpaw")} icon="archive">
				REPOSITORY
			</IconButton>
		</div>
	</div>
</div>

<style>
	.TopMenu{
		padding: 1rem;
		border-bottom: 1px solid var(--main-horizontalLine-color);
	}
</style>