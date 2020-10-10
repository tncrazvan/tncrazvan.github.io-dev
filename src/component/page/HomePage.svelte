<script>
import IconButton from '../button/IconButton.svelte';
</script>

<div class="row mt-5">
	<div class="grid-x-center">
		<h5>Website moved, nothing to see here.</h5>
		<IconButton icon="link" onClick={()=>window.location.href="http://razshare.net"}>
			Visit new website
		</IconButton>
	</div>
</div>