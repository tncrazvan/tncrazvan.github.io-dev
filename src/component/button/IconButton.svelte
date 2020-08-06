<script>
export let icon;
export let onClick;
export let ignoreText=false;
let cls; export {cls as class};
</script>
<div on:click={onClick} class="waves-effect btn btn-flat{cls?' '+cls:''}">
	{#if icon && icon !== ""}
		<i class="relative material-icons {ignoreText?'':'adjust'}">{icon}</i>
	{/if}
	{#if !ignoreText}
	<span class="relative {icon?'adjust':''}"><slot></slot></span>
	{/if}
</div>

<style>
	.btn span.adjust{
		top: -0.32rem;
	}
</style>