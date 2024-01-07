<script lang="ts">
	import '@aircss/air';

	import Modal from '$lib/modal.svelte';
	import Dispatch from './dispatch.svelte';

	let modal: Modal;
	let params: { email: string };

	function imperative() {
		modal.show({ value: 'value@func' });
	}

    function emptyrative() {
		modal.show();
	}

	$: console.log(params);
</script>

<Modal
	bind:this={modal}
	class="w6 ba bg--white"
	on:success={console.log}
	on:cancel={console.warn}
	bind:params
>
	<h2 class="ma0 pa4 bb b--noir-20">Confirm</h2>

	<div class="ph4">
		<p class="lh-body tj i">Do you confirm the pending operation ?</p>
	</div>

	<div class="flex pa4 bt b--noir-20 evenly-filled">
		<button class="w4 pa3 ba bg--red white pointer tc" on:click={modal.close}> No </button>

		<button
			class="w4 pa3 ba bg--emeraude white pointer tc"
			data-success="true"
			on:click={modal.close}
		>
			Yes
		</button>
	</div>
</Modal>

<button on:click={modal.show}>Direct event</button>
<button data-value="value@attr" on:click={modal.show}>Direct event w/ value</button>

<button on:click={emptyrative}>Call function</button>
<button on:click={imperative}>Call function w/ value</button>

<Dispatch on:nosignal={modal.show} on:signal={modal.show} />
