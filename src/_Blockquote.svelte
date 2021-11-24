<script>
	export let indent;
</script>


{#if indent === 0}
	<slot></slot>
{:else}
	<blockquote>
		<svelte:self indent={indent-1}>
			<slot></slot>
		</svelte:self>
	</blockquote>
{/if}
