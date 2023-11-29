<script>
    import { onMount } from "svelte";
    import Dialog from "$lib/Dialog/Dialog.svelte";
    import {tick} from 'svelte';

    /**
     * @type {{ showModal: () => void; close: () => void; }}
     */
    let dialog;

    // Declaring the variable(s) used to show and hide the dialog
    let showDialog = false;

    // Declaring  a list of buttons that will appear in the footer of the dialog
    let footerButtons = [
        {label: "Cancel", code: "cancel"},
        {label: "Clear", code: "clear"},
        {label: "Submit", code: "submit"}
    ]


    // A function that will show the dialog
    async function openDialog() {
        showDialog = true;
        await tick(); // waits for dialog to be set
        dialog.showModal();
    }

    // A function that will hide the dialog
    function hideDialog() {
        dialog.close();
        showDialog = false;
    }

    /**
     * A function to handel all the footerButtons for the dialog
     * @param {{ detail: { code: string; }; }} e
     */
    function handleFooterButton(e) {
        if(e.detail && e.detail.code === 'cancel') {
            // handle cancel
        }
        if(e.detail && e.detail.code === 'clear') {
            // handle clear
        }
        if(e.detail && e.detail.code === 'submit') {
            // handle submit
        }
        hideDialog();
    }

    /**
     * A function to handel escape key pressed
     */
    function handleEscape() {
        // handle escape
        hideDialog();
    }

</script>

<!-- The imported dialog component  -->
{#if showDialog}
  <Dialog 
        bind:dialog 
        headerText={"Your header text"} 
        {footerButtons}
        on:footerButtonHandler={handleFooterButton} 
        on:escapePressed={handleEscape}
    >
    Some text or html here that will be passed in via a slot
  </Dialog>
{/if}
<button on:click={openDialog}>Open</button>

<style>
    
</style>
