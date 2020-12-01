<script lang="ts">
import ExampleComponent from "../components/ExampleComponent.svelte";

import {
  Button,
  Card,
  CardText,
  CardActions,
} from "svelte-materialify";

let theme: "light" | "dark" = "dark";

function toggleTheme() {
  if (theme === "light") theme = "dark";
  else theme = "light";
}
</script>

<style>
.centerer {
  @apply flex-1 flex flex-col items-center justify-center;
}
</style>




<div class:centerer="{true}">
  <!-- Here's how you could extract conditional class groups with @apply -->
  <Button rounded class="secondary-color" on:click="{toggleTheme}">
    Toggle
    {theme === 'light' ? 'dark' : 'light'}mode
  </Button>
  <div class="justify-center mt-4 mb-4 d-flex">
    <Card outlined style="max-width:300px;">
      <div class="pt-3 pl-4 pr-4">
        <span class="text-overline"> OVERLINE </span>
        <br />
        <span class="mb-2 text-h5">Headline</span>
        <br />
      </div>
      <CardText>
        Lorem ipsum dolor sit amet consectetur adipisicing elit.
        Reprehenderit, qui quaerat rerum incidunt nisi ducimus?
      </CardText>
      <CardActions>
        <Button rounded outlined>Button</Button>
      </CardActions>
    </Card>
  </div>
  <ExampleComponent
    title="🌐 Opinionated Sapper project base"
    paragraph="This is an example route and component to make sure everything's working."
  />
  <a
    class="p-3 mt-10 transition duration-200 ease-in-out rounded-lg shadow-md focus:outline-none focus:shadow-outline"
    href="/graphql"
  >
    Check out the GraphQL playground!
  </a>
</div>