<script lang="ts">
  import {
    getAanNames,
    getAanAccountAddress,
  } from "@freddyblockchain/aans-utils";
  import TextInput from "./TextInput.svelte";
  import Button from "./Button.svelte";

  let value = "";
  let correspondingAddress: string | undefined = "";

  const lookupaan = async () => {
    correspondingAddress = await getAanAccountAddress(value);
  };

  let namesPromise = getAanNames();
</script>

<div class="flex justify-center items-center border-gray-100 border-4 p-8">
  <TextInput placeholder="aan" bind:value />
  <Button placeholder={"Lookup aan"} buttonPressedAction={lookupaan} />
  <TextInput
    placeholder="Corresponding Address"
    bind:value={correspondingAddress}
    editable={false}
  />
</div>
{#await namesPromise then names}
  <h3>Existing Algorand Alias Names</h3>
  <textarea disabled={true}>{names}</textarea>
{/await}

<style>
  textarea {
    /* Set the size of the textarea */
    height: 300px; /* Example height */
    width: 60%; /* Example width, relative to its container */

    /* Center the textarea */
    display: block; /* Block display is necessary for margin auto to work */
    margin: 20px auto; /* Vertical margins to 20px and horizontal margins auto for centering */

    /* Additional styling */
    resize: none; /* Prevent resizing. Remove this line if you want the user to resize it */
    padding: 10px; /* Optional: Adds some padding inside the textarea */
    font-family: Arial, sans-serif; /* Optional: Changes the font */
    font-size: 16px; /* Optional: Changes the font size */
    border-radius: 8px; /* Optional: Adds rounded corners */
    border: 1px solid #ccc; /* Optional: Adds a border */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Optional: Adds a slight shadow for depth */
  }
  h3 {
    text-align: center;
  }
</style>
