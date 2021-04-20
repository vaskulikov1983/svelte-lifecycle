<script>
    import {createEventDispatcher} from 'svelte';
    export let title;
    export let price;
    export let bestseller = false;

    const dispatch = createEventDispatcher();
    const deleteEvent = () => dispatch('delete', 'p1');
</script>

<article on:click>
    <h1>{title}</h1>
    <h2>${price}</h2>
    {#if bestseller}
        <h3>Bestseller</h3>
    {/if}
    <button on:click={() => dispatch('add-to-cart', {id: 'p1'})}>Add to Cart</button>
    <button on:click={deleteEvent}>Delete</button>
</article>