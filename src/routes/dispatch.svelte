<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

    function nosignal() {
		dispatch('nosignal', {});
	}

	function signal() {
		dispatch('signal', { value: 'value@detail' });
	}
</script>

<button on:click={nosignal}>Dispatch event</button>

<button on:click={signal}>Dispatch event w/ payload</button>
