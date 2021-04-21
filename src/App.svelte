<script>
	import Product from "./Product.svelte";
	import Modal from "./Modal.svelte";
	import { tick } from "svelte";

	const addToCart = (event) => {
		console.log(event);
	}

	const deleteFromCart = (evt) => {
		console.log(evt.detail);
	}

	const products = [
		{
			id: 'p1',
			title: 'A book',
			price: 9.99,
			bestseller: true
		}
	];

	const transform = async (evt) => {
		if (evt.which !== 9) return;

		evt.preventDefault();

		const selectionStart = evt.target.selectionStart;
		const selectionEnd = evt.target.selectionEnd;
		const value = evt.target.value;

		text = value.slice(0, selectionStart) +
			   value.slice(selectionStart, selectionEnd).toUpperCase() +
			   value.slice(selectionEnd); 

		await tick();

		evt.target.selectionStart = selectionStart;
		evt.target.selectionEnd = selectionEnd;
	};

	let showModal = false;
	let closeable = false;
	let text = "This is how it works!";

</script>

<style>

</style>

{#each products as product}
	<Product
		{...product}
		on:add-to-cart={addToCart}
		on:delete={deleteFromCart}
	/>
{/each}

<button on:click={() => showModal = true}>Show modal</button>

{#if showModal}
<Modal 
	on:cancel={() => showModal = false}
	on:close={() => showModal = false}
	let:didAgree = {closeable}
	>
	<h1 slot="header">Hello!</h1>
	<p>This is how it works</p>
	<button slot="footer" on:click={() => showModal = false} disabled={!closeable}>Confirm</button>
</Modal>
{/if}

<textarea rows="10" value={text} on:keydown="{transform}"></textarea>



