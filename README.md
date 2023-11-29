# svelte-dialog-component

## Installation

1. Ensure you have node installed on your OS (v19 and above - recommended)
2. Navigate to the app where you would like to use the component and run the following in your terminal
```bash
npm install svelte-dialog-component --save
```

## How to use the component

1. Inside the script tag of your .svelte file 
```javascript
import { Dialog } from 'svelte-dialog-component'
```
2. Inside an HTML element use the imported Menu component like so
```javascript
<Dialog 
        bind:dialog 
        headerText={"Your header text"} 
        {footerButtons}
        on:footerButtonHandler={handleFooterButton} 
        on:escapePressed={handleEscape}
    >
    Some text or html here that will be passed in via a slot
  </Dialog>
```

## Props, handlers
1. ```bind:dialog``` Required
2. ```headerText={"Your header text"}``` Optional, String to display as header text
3. ```{footerButtons}``` Optional, Array of objects
4. ```on:footerButtonHandler={handleFooterButton}``` Optional, Function to handle te events emited by the footerButtons
4. ```on:escapePressed={handleEscape}``` Optional, a function to handle the behaviour of the dialog when the Escape key is pressed


## Example
```+layout.svelte```
``` javascript
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
```


## Styling
Can be set with variables associated with every element
```css
--dialogContainerBackgroundColor
--dialogHeaderColor
--dialogFooterFirstButtonBackgroundColor
--dialogFooterFirstButtonColor
--dialogFooterFirstButtonHoverBackgroundColor
--dialogFooterButtonBorder
--dialogFooterButtonColor
--dialogFooterButtonHoverBorder
```

## Feedback and recommendations
Please send me feedback or recommendations for improvements at mariusrossouwcr@gmail.com. I would love to here from you. [Donations](https://www.paypal.com/paypalme/MariusFRossouw) are welcome but not necessary.


