<script>
	import Product from "./Product.svelte";
	import Modal from "./Modal.svelte";

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

	let showModal = false;
	let closeable = false;

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



