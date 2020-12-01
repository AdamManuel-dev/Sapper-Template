<script context="module">
export const preload = () => {};
</script>

<script>
import { stores } from "@sapper/app";

import {
  MaterialApp,
  NavigationDrawer,
  List,
  ListItem,
  Avatar,
  Divider,
  Icon,
  Footer
} from "svelte-materialify";

let mini = true;
function mouseenter() {
  mini = false;
}
function mouseleave() {
  mini = true;
}

let theme: "light" | "dark" = "dark";

function toggleTheme() {
  if (theme === "light") theme = "dark";
  else theme = "light";
}

// You may not want to use `segment`, but it is passed for the time being and will
// create a warning if not expected: https://github.com/sveltejs/sapper-template/issues/210
// https://github.com/sveltejs/sapper/issues/824
export let segment: string = "";
// Silence unused export property warning
if (segment) {
}

const { page } = stores();

let path: string;
$: path = $page.path.slice(1);
</script>

<svelte:head>
  <title>{path ? path.charAt(0).toUpperCase() + path.slice(1) : 'Index'}</title>
</svelte:head>

<MaterialApp theme="{theme}">
  <div class="flex flex-row h-screen">
    <div
      class="h-full d-inline-block"
      on:mouseenter="{mouseenter}"
      on:mouseleave="{mouseleave}"
    >
      <NavigationDrawer mini="{mini}">
        <ListItem>
          <span slot="prepend" class="ml-n2">
            <Avatar size="{40}">
              <img src="//picsum.photos/200" alt="profile" />
            </Avatar>
          </span>
          Adam Manuel
        </ListItem>
        <Divider />
        <List dense nav>
          <a href="/">
            <ListItem>
              <span slot="prepend" class="ml-n1">
                <!-- <Icon class="mdi mdi-home-city" /> -->
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-6">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
                </svg>
              </span>
              <span class="ml-4">Home</span>
            </ListItem>
          </a>
          <a href="/drag-drop">
            <ListItem>
              <span slot="prepend" class="ml-n1">
                <!-- <Icon class="mdi mdi-home-city" /> -->
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-6">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 11.5V14m0-2.5v-6a1.5 1.5 0 113 0m-3 6a1.5 1.5 0 00-3 0v2a7.5 7.5 0 0015 0v-5a1.5 1.5 0 00-3 0m-6-3V11m0-5.5v-1a1.5 1.5 0 013 0v1m0 0V11m0-5.5a1.5 1.5 0 013 0v3m0 0V11" />
                </svg>
              </span>
              <span class="ml-4">Drag</span>
            </ListItem>
          </a>
          <!-- <ListItem>
            <span slot="prepend">
              <Icon class="mdi mdi-account" />
            </span>
            Account
          </ListItem>
          <ListItem>
            <span slot="prepend">
              <Icon class="mdi mdi-account-group" />
            </span>
            Users
          </ListItem> -->
        </List>
      </NavigationDrawer>
    </div>
    <div class="flex flex-col w-full">
      <slot />
      <Footer class="justify-center pa-2" padless>Built with ♥</Footer>
    </div>
  </div>
</MaterialApp>
