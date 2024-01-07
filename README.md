# Modal dialog

`svelte-modal` is a simple modal dialog based on aircss and svelte.

## Installation

In an existing svelte project, simply run the following command:

```bash
npm add @aircss/svelte-modal
```

## Usage

The following example is a page with a basic "two-buttons" confirmation dialog and a clickable button to show it:

```svelte
<script lang="ts">
	import '@aircss/air';

	import Modal from '@aircss/svelte-modal';

	let modal;
</script>

<Modal bind:this={modal} class="w6 ba bg--white" on:success={console.log} on:cancel={console.warn}>
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

<button on:click={modal.show}>Show</button>
```

### Props

- **`id`**: set a id attribute to the model element _(optional)_
- **`class`**: set custom classes for the modal element _(optional)_
- **`params`**: bi-directional binding to share anything between caller and callee _(optional)_

### Methods

- **`show(payload: unknown)`**: make the modal visible and set its `params` prop with the passed argument.
  If the method is called by an HTML event (like a click on a button element), `show()` will use the
  data attributes of the event target if there is any.

- **`close(payload: unknown)`**: make the modal disappear. The custom event triggered by closing the
  modal will use the payload as its `detail`. If the method is called by an HTML event (like a click
  on a button element), `close()` will use the data attributes of the event target if there is any.

### Events

- **`show`**: this event is fired anytime the modal is made visible. `event.detail` holds the
  `params` argument of the _ad-hoc_ method if set.

- **`close`**: this event is fired anytime the modal disappears. `event.detail` holds the
  `payload` of the _ad-hoc_ method if set _(through method args or data attributes of the event target)_.

- **`success`**: this event is fired when the modal disappears and if the `close()` method has
  a payload _(through method args or data attributes of the event target)_.

- **`cancel`**: this event is fired when the modal disappears and if the `close()` method has
  no payload _(through method args or data attributes of the event target)_.
