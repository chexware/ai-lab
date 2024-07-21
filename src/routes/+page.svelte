<script lang="ts">
  import { onMount } from 'svelte';
  import { Textarea } from '$lib/components/ui/textarea';
  import * as Tabs from '$lib/components/ui/tabs';
  //import * as Form from '$lib/components/ui/form';
  import { Label } from '$lib/components/ui/label';
  import { Input } from '$lib/components/ui/input';
  import * as Card from '$lib/components/ui/card/index';
  import { Button } from '$lib/components/ui/button/index';
  import OpenAI from 'openai';


  const authorizedFileExtensions = ['image/jpg', 'image/jpeg', 'image/png', 'image/webp'];
  
  // State Bindings
  let imageFile = '';
  let description = '';
  let isLoading = false;
 
  function handleImageUpload(event: any) {
   const file = event.target.files[0];
   if (file) {
      const reader = new FileReader();
      reader.onloadend = () => {
         const base64Data = reader.result;
         if (base64Data) imageFile = base64Data.toString();
      };
      reader.readAsDataURL(file);
   }
  }

  const handleTextGeneration = async () => {
   isLoading = true;
   const response = await fetch('http://127.0.0.1:7860/interrogator/prompt',{
      method: 'POST',
      headers: {
         'Content-Type': 'application/json',
      },
      body: JSON.stringify({
         image: imageFile,
         clip_model_name: 'ViT-L-14/openai',
         mode: 'fast',
      }),
   });
   const data = await response.json();
   description = data.prompt;
   isLoading = false;
  }
 
  $: imageFile
  $: description
  $: isLoading
</script>


<Tabs.Root value="computer-vision" class="bg-gray-dark p-10">
   <Tabs.List class="grid w-full grid-cols-3 bg-gray-light">
      <Tabs.Trigger value="computer-vision">Computer Vision</Tabs.Trigger>
      <Tabs.Trigger value="text-generation">Text Generation</Tabs.Trigger>
      <Tabs.Trigger value="image-generation">Image Generation</Tabs.Trigger>
   </Tabs.List>
   <Tabs.Content value="computer-vision" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      <Card.Root class="mx-3 bg-blue rounded-lg h-[580px] text-center">
         <Card.Header>
           <Card.Title>Image Processing</Card.Title>
           <Card.Description>Generating a story based on an image description</Card.Description>
         </Card.Header>
         <Card.Content >
            <div class="flex w-1/2 items-center space-x-2">
               <Label for="file">Select Image</Label>
               <Input type="file" accept={authorizedFileExtensions.join(',')} id="file" name="file" on:change={handleImageUpload}/> 
            </div>
            {#if imageFile }
               <img src={imageFile} alt="Uploaded Image" class="pt-10"/>
               <Button class="mt-5" on:click={handleTextGeneration}>Generate Description</Button> 
            {/if}
            {#if description && !isLoading }
               <Label for="image-description">Descritpion: </Label>
               <Textarea disabled id="image-description" placeholder={description} />
            {/if}
         </Card.Content>
       </Card.Root>
   </Tabs.Content>
   <Tabs.Content value="text-generation" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      <Card.Root class="mx-3 bg-blue rounded-lg h-[580px] text-center">
         <Card.Header>
           <Card.Title>Story Generator</Card.Title>
           <Card.Description>Generating a story based on an image description</Card.Description>
         </Card.Header>
         <Card.Content >
            <Button>Generate Story</Button> 
         </Card.Content>
       </Card.Root>
   </Tabs.Content>
   <Tabs.Content value="image-generation" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      <Card.Root class="mx-3 bg-blue rounded-lg h-[580px] text-center">
         <Card.Header>
           <Card.Title>Image Generator</Card.Title>
           <Card.Description>Generating image based on a given story</Card.Description>
         </Card.Header>
         <Card.Content>
            <Button>Generate Image</Button>
         </Card.Content>
      </Card.Root>
   </Tabs.Content>
</Tabs.Root>    


<style lang="postcss">
   :global(html) {
     background-color: theme(colors.gray-dark);
     color: theme(colors.gray);
   }
</style>


