<script lang="ts">
  //import { Textarea } from "$lib/components/ui/textarea";
  import * as Tabs from "$lib/components/ui/tabs";
  //import * as Form from "$lib/components/ui/form";
  //import { Input } from "$lib/components/ui/input";
  import * as Card from "$lib/components/ui/card/index";
  import { Button } from "$lib/components/ui/button/index";
</script>


<Tabs.Root value="computer-vision" class="bg-gray-dark p-10">
   <Tabs.List class="grid w-full grid-cols-3 bg-gray-light">
      <Tabs.Trigger value="computer-vision">Computer Vision</Tabs.Trigger>
      <Tabs.Trigger value="text-generation">Text Generation</Tabs.Trigger>
      <Tabs.Trigger value="image-generation">Image Generation</Tabs.Trigger>
   </Tabs.List>
   <Tabs.Content value="computer-vision" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      Hello
   </Tabs.Content>
   <Tabs.Content value="text-generation" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      <Card.Root class="mx-3 bg-blue rounded-lg h-[580px] text-center">
         <Card.Header>
           <Card.Title>Story Generator</Card.Title>
           <Card.Description>Generating a story based on an image description</Card.Description>
         </Card.Header>
         <Card.Content>
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


