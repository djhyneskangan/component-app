<script>
    import { Button, Modal, Label, Input, Checkbox, Textarea, Fileupload } from 'flowbite-svelte';
    import { createEventDispatcher } from 'svelte';

    let textArea;
    let formModal = false;
    let photoUpload = ('None');

    const dispatch = createEventDispatcher();

    function handleAddClick(event) {
      dispatch(
        "newEntry",
        {
          text: textArea
        }
      );

      formModal = false;
    }

  </script>
  
  <Button on:click={() => formModal = true}>New Entry</Button>
  
  <Modal bind:open={formModal} size="xs" autoclose={false} class="w-full">
    <form class="flex flex-col space-y-6" action="#">
      <h3 class="mb-4 text-xl font-medium text-gray-900 dark:text-white">Add new journal entry</h3>
      <Label class="space-y-2"> 
      <Label for="textarea-id" class="mb-2 space-y-2">Your message</Label>
        <Textarea bind:value={textArea} id="textarea-id" placeholder="Your message" rows="4" name="message"/>
        <Label class="space-y-2 mb-2">
            <span>Upload file</span>
            <Fileupload bind:photoUpload />
          </Label>
          <Label>File: {photoUpload }</Label>
      </Label>
      <Button class="w-full1" on:click={handleAddClick}>Add</Button>
    </form>
  </Modal>