<script>
	import {onMount} from 'svelte';
	export let language="html";
	let code;
	onMount(()=>{
		hljs.highlightBlock(code);
	});
</script>

<pre><code bind:this={code} class="{language} selectable"><slot></slot></code></pre>

<style>
	pre{
		display: inline-block;
		top: 0.85rem;
		position: relative;
		border: 1px solid var(--main-horizontalLine-color);
	}
	.hljs{
		background: rgba(0,0,0,0.25);
	}
</style>