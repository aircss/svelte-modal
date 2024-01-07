<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let _class = '';
	let visible = false;

	export { _class as class };
	export let id: string | undefined = undefined;
	export let params: unknown = undefined;

	export function show(this: unknown, payload?: unknown) {
		const event = payload as CustomEvent;

		// FIXME: workaround to remove an undocumented dataset property added
		// by svelte.
		const {svelteH: _, ...dataset} = (this as HTMLElement)?.dataset || {}
		const detail = { ...(event?.detail || payload) };

		if (Object.keys(dataset).length !== 0) {
			params = dataset;
		} else if (Object.keys(detail).length !== 0) {
			params = detail
		}

		visible = true;
		dispatch('show', params);
	}

	export function close(this: unknown, payload?: unknown) {
		const event = payload as CustomEvent;

		// FIXME: workaround to remove an undocumented dataset property added
		// by svelte.
		const {svelteH: _, ...dataset} = (this as HTMLElement)?.dataset || {}
		const detail = { ...(event?.detail || payload) };

		visible = false;
		if (Object.keys(dataset).length !== 0) {
			dispatch('success', dataset);
			dispatch('close', dataset);
		} else if (Object.keys(detail).length !== 0) {
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
				<slot {params} />
			</div>
		</div>
	</div>
{/if}
