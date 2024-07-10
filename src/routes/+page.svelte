<script lang="ts">
  import { Textarea } from "$lib/components/ui/textarea";
  import * as Tabs from "$lib/components/ui/tabs";
  //import * as Card from "$lib/components/ui/card/index";
</script>


<Tabs.Root value="computer-vision" class="bg-gray-dark p-10">
   <Tabs.List class="grid w-full grid-cols-3 bg-gray-light">
      <Tabs.Trigger value="computer-vision">Computer Vision</Tabs.Trigger>
      <Tabs.Trigger value="text-generation">Text Generation</Tabs.Trigger>
      <Tabs.Trigger value="image-generation">Image Generation</Tabs.Trigger>
   </Tabs.List>
   <Tabs.Content value="computer-vision" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      Make changes to your account here 1.
   </Tabs.Content>
   <Tabs.Content value="text-generation" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      Make changes to your account here 2.
   </Tabs.Content>
   <Tabs.Content value="image-generation" class="pt-3 bg-gray-light rounded-sm h-[600px] text-center">
      Make changes to your account here 3.
   </Tabs.Content>
</Tabs.Root>    


<style lang="postcss">
   :global(html) {
     background-color: theme(colors.gray-dark);
     color: theme(colors.gray);
   }
   
</style>


