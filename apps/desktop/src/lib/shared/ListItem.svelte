<script lang="ts">
	import Icon from '@gitbutler/ui/Icon.svelte';
	import type iconsJson from '@gitbutler/ui/data/icons.json';
	import type { Snippet } from 'svelte';

	interface Props {
		icon?: keyof typeof iconsJson | undefined;
		selected?: boolean;
		loading?: boolean;
		children?: Snippet;
		onClick?: () => void;
	}

	const {
		icon = undefined,
		selected = false,
		loading = false,
		children,
		onClick
	}: Props = $props();
</script>

<button type="button" disabled={selected} class="button" class:selected onclick={() => onClick?.()}>
	<div class="label text-14 text-bold">
		{@render children?.()}
	</div>
	{#if icon || selected}
		<div class="icon">
			{#if icon}
				<Icon name={loading ? 'spinner' : icon} />
			{:else}
				<Icon name="tick" />
			{/if}
		</div>
	{/if}
</button>

<style lang="postcss">
	.button {
		display: flex;
		align-items: center;
		color: var(--clr-scale-ntrl-10);
		font-weight: 700;
		padding: 10px 10px;
		justify-content: space-between;
		border-radius: var(--radius-m);
		width: 100%;
		transition: background-color var(--transition-fast);

		&:hover:enabled,
		&:focus:enabled {
			background-color: var(--clr-bg-1-muted);
			& .icon {
				color: var(--clr-scale-ntrl-40);
			}
		}
		&:disabled {
			background-color: var(--clr-bg-2);
			color: var(--clr-text-2);
		}
		& .icon {
			display: flex;
			color: var(--clr-scale-ntrl-50);
		}
		& .label {
			height: 16px;
			text-overflow: ellipsis;
			overflow: hidden;
		}
	}
</style>
