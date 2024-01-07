<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let _class = '';
	let visible = false;

	export { _class as class };
	export let id: string | undefined = undefined;
	export let params: unknown = undefined;

	export function show(this: HTMLElement, payload: unknown) {
		const detail = { ...(this.dataset || payload) };

		if (Object.keys(detail).length !== 0) {
			params = detail;
		}

		visible = true;
		dispatch('show', params);
	}

	export function close(this: HTMLButtonElement, payload: unknown) {
		const detail = { ...(this.dataset || payload) };

		visible = false;
		if (Object.keys(detail).length === 0) {
			dispatch('cancel');
			dispatch('close');
		} else {
			dispatch('success', detail);
			dispatch('close', detail);
		}
	}
</script>

{#if visible}
	<div {id} class="fixed flex top left w-100 h-100 z-999 evenly-spaced" aria-hidden="true">
		<div class="center">
			<div class={_class}>
				<slot {params} />
			</div>
		</div>
	</div>
{/if}
