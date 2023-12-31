<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let _class = '';
	let visible = false;

	export { _class as class };
	export let id: string | undefined = undefined;

	export function show() {
		visible = true;
		dispatch('show');
	}

	export function close(this: HTMLButtonElement, rv: any) {
		const detail = this?.dataset.value || rv;
		visible = false;
		if (detail) {
			dispatch('success', detail);
			dispatch('close', detail);
		} else {
			dispatch('cancel');
			dispatch('close');
		}
	}
</script>

{#if visible}
	<div {id} class="fixed flex top left w-100 h-100 z-999 evenly-spaced" aria-hidden="true">
		<div class="center">
			<div class={_class}>
				<slot />
			</div>
		</div>
	</div>
{/if}
