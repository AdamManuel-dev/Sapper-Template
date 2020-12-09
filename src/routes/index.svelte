<script context="module">
  export const preload: Preload.Preload = async function (this, page, session) {
    return { path: page };
  };
</script>

<script>
  import ExampleComponent from "../components/ExampleComponent.svelte";
  import type { Preload } from "@sapper/common";

  export let path: Preload.Page;
</script>

<style>
  .centerer {
    @apply flex-1 flex flex-col items-center justify-center;
  }
</style>

<div class:centerer="{true}">
  <!-- Here's how you could extract conditional class groups with @apply -->
  <ExampleComponent
    title="🌐 Opinionated Sapper project base"
    paragraph="This is an example route and component to make sure everything's working."
  />
  <pre>{JSON.stringify(path, undefined, 2)}</pre>
</div>
