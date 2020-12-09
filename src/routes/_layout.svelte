<script context="module">
  export const preload: Preload.Preload = async function (this, page, session) {
    return {};
  };
</script>

<script>
  import type { Preload } from "@sapper/common";
  import { stores } from "@sapper/app";

  let mini = true;

  function mouseenter() {
    mini = false;
  }
  function mouseleave() {
    mini = true;
  }

  // You may not want to use `segment`, but it is passed for the time being and will
  // create a warning if not expected: https://github.com/sveltejs/sapper-template/issues/210
  // https://github.com/sveltejs/sapper/issues/824
  export let segment: string = "";
  // Silence unused export property warning
  if (segment) {
  }

  const { page } = stores();

  let _path: string;
  $: _path = $page.path.slice(1);
</script>

<style>
  .small {
    @apply w-12;
  }

  .large {
    @apply w-64;
  }
</style>

<svelte:head>
  <title>
    {_path ? _path.charAt(0).toUpperCase() + _path.slice(1) : 'Index'}
  </title>
</svelte:head>

<div class="flex flex-row h-screen">
  <div
    class="absolute h-full transition-all duration-150 ease-in-out bg-red-200 d-inline-block"
    class:small="{mini}"
    class:large="{!mini}"
    on:mouseenter="{mouseenter}"
    on:mouseleave="{mouseleave}"
  >
    <pre>
      MENU
    </pre>
  </div>
  <div class="flex flex-col w-full ml-12 bg-gray-200">
    <slot />
  </div>
</div>
