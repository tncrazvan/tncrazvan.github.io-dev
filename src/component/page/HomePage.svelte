<script>
import SectionTitle from './../text/SectionTitle.svelte';
import IconButton from '../button/IconButton.svelte';
import Coding from './../highlighter/Coding.svelte';
import { fly, fade } from 'svelte/transition';
import Spinner from '../Spinner.svelte';

let promise = getData();

async function getData(){
	const REGEX = /^\<\?php\r?\n?/g;
	let data = {
		location: "tncrazvan/catpaw-template",
		main: (await (await fetch("/docs/main.php")).text()).replace(REGEX,""),
		event_1: (await (await fetch("/docs/event_1.php")).text()).replace(REGEX,""),
		event_1_2: (await (await fetch("/docs/event_1_2.php")).text()).replace(REGEX,""),
		event_2: (await (await fetch("/docs/event_2.php")).text()).replace(REGEX,""),
		home_page: (await (await fetch("/docs/HomePage.php")).text()).replace(REGEX,""),
		websocket_test: (await (await fetch("/docs/WebSocketTest.php")).text()).replace(REGEX,""),
		websocket_test_constructor_only: (await (await fetch("/docs/WebSocketTest_constructor_only.php")).text()).replace(REGEX,""),
		http_consumer_example: (await (await fetch("/docs/http_consumer_example.php")).text()).replace(REGEX,""),
		index: (await (await fetch("/docs/index.php")).text())
	};

	return data;
}
</script>


{#await promise}
<div class="max-full full-height grid-x-center grid-y-center" transition:fade={{duration: 250}}>
	<!-- <SpinnerElipsis /> -->
	<Spinner />
</div>
{:then data}
<div class="row mt-5">
	<div class="grid-x-center">
		<h5>Website moved, nothing to see here.</h5>
		<IconButton icon="link" onClick={()=>window.location.href="http://razshare.net"}>
			Visit new website
		</IconButton>
	</div>
</div>
{/await}