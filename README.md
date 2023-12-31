# Modal dialog

``svelte-modal`` is a simple modal dialog based on aircss and svelte.


## Installation

In an existing svelte project, simply run the following command:

```bash
npm add @aircss/svelte-modal
```

## Usage

The following example is a page with a basic "two-buttons" modal and a
clickable button to show it:

```html
<script lang="ts">
	import '@aircss/air';

	import Modal from '@aircss/svelte-modal';

	let modal;
</script>

<Modal
	bind:this={modal}
	class="w6 br3 ba b--noir-20 bg--white shadow"
	on:success={console.log}
	on:cancel={console.warn}
>
	<h2 class="ma0 pa4 bb b--noir-20">Modal title</h2>

	<div class="ph4">
		<p class="lh-body tj i">
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Ex eius eligendi suscipit sapiente,
			perferendis tenetur, quos, non odit hic provident excepturi consequatur fugit omnis rem ea
			cumque laboriosam debitis vero.
		</p>
	</div>

	<div class="flex pa4 bt b--noir-20 evenly-filled">
		<button class="w4 pa3 ba b--noir-30 bg--white noir-60 f6 b pointer tc" on:click={modal.close}>
			Cancel
		</button>

		<button
			class="w4 pa3 ba b--blue bg--blue white f6 b pointer tc"
			data-value="true"
			on:click={modal.close}
		>
			Validate
		</button>
	</div>
</Modal>

<button class="w4 pa3 ba b--noir-30 bg--white noir-60 f6 b pointer tc" on:click={modal?.show}>
	Show modal
</button>
```
