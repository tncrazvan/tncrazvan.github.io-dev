<script>
	import {onMount} from 'svelte';
	export let language="html";
	export let padding;
	export let style;
	let code;
	onMount(()=>{
		hljs.highlightBlock(code);
	});
</script>

<pre {style}><code bind:this={code} style="{(padding?"padding:"+padding+";":"")}" class="{language} selectable"><slot></slot></code></pre>

<style>
	pre{
		max-width: 100%;
		display: inline-block;
		top: 0.4rem;
		position: relative;
		border: 0px solid var(--main-horizontalLine-color);
		margin: 0;
	}
	code{
		padding-top: 0;
		padding-bottom: 0;
	}
	@media screen and (max-width: 980px) {
		pre{
			display: block;
			margin-bottom: 0.8rem;
		}
		code{
			padding: 0.3rem;
		}
   }
	.hljs{
		background: rgba(0,0,0,0.25);
	}
</style>