<script>
    import {createEventDispatcher, onMount, onDestroy, beforeUpdate, afterUpdate} from "svelte";
    const dispatch = createEventDispatcher();

    const cancel = () => {dispatch('cancel')};
    const close = () => {dispatch('close')};

    let agree = false;
    let autoscroll = false;

    onMount(() => {
        console.log('onMount');
    });

    onDestroy(() => {
        console.log('onDestroy');
    })

    beforeUpdate(() => {
        console.log('beforeUpdate');
        autoscroll = agree;
    });

    afterUpdate(() => {
        console.log('afterUpdate');
        if (autoscroll) {
            const modal = document.querySelector('.modal');
            modal.scrollTo(0, modal.scrollHeight);
        }
    });

    console.log('Script executed!');
</script>

<style>
    .backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.75);
  z-index: 10;
}

.modal {
  padding: 1rem;
  position: fixed;
  top: 10vh;
  left: 10%;
  width: 80%;
  max-height: 15vh;
  background: white;
  border-radius: 5px;
  z-index: 100;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  overflow: scroll;
}

header {
    border-bottom: 1px solid rgb(56, 56, 56);
}

</style>

<div class="backdrop" on:click={cancel}></div>
<div class="modal">
    <header>
        <slot name="header"></slot>
    </header>
    <div class="content">
        <slot></slot>
    </div>
    <div>
        <p>Before you can confirm this, you have to agree our terms!</p>
        <button on:click={() => agree = true}>Agree</button>
    </div>
    <footer>
        <slot name="footer" didAgree={agree}>
            <button on:click={close} disabled={!agree}>Close</button>
        </slot>
    </footer>
</div>