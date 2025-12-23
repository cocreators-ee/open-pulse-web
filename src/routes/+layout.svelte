<script lang="ts">
  import {page} from '$app/state';
  import {goto} from '$app/navigation';

  import '@fontsource-variable/merriweather-sans';
  import '$style/setup.scss';
  import Container from "$lib/Container.svelte";

  let {children} = $props();
  let currentPath = $derived(page.url.pathname);
</script>

<nav>
  <Container>
    <div class="nav-items">
      <div class="link"
           class:selected={currentPath === "/"}
           onclick={() => goto("/")}
           onkeydown={() => goto("/")}
           role="button"
           tabindex="0">
        Home
      </div>
      <div class="link"
           class:selected={currentPath === "/privacy/"}
           onclick={() => goto("/privacy/")}
           onkeydown={() => goto("/privacy/")}
           role="button"
           tabindex="0">
        Privacy
      </div>
      <a class="link" href="https://github.com/cocreators-ee/open-pulse-app" target="_blank" rel="noopener">
        Source code
      </a>
    </div>
  </Container>
</nav>

<main>
  {@render children()}
</main>

<footer>
  <Container>
    <p>Built with ❤️ from Estonia by Cocreators OÜ</p>
    <p>Copyright &copy; Cocreators OÜ, 2025</p>
    <a href="https://github.com/cocreators-ee/open-pulse-web" target="_blank" rel="noopener">
      Website source code
    </a>
  </Container>
</footer>

<style lang="scss">
  @use "variables" as *;

  :global(body, html) {
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    background: $blue-deep;
  }

  nav {
    background: $blue-dark;

    .nav-items {
      display: flex;
      flex-direction: row;

      .link {
        display: flex;
        flex-direction: column;
        color: $text-light;
        text-decoration: none;

        $size: 48px;
        height: $size;

        padding: 0 $spacing-4;

        align-items: center;
        justify-content: center;
        position: relative;

        border: 1px solid transparent;

        &.selected {
          background: $blue-vibrant;
          border: 1px solid $border-color;
        }
      }
    }
  }

  main {
    flex-grow: 1;
  }

  footer {
    display: flex;
    flex-direction: row;
    padding: $spacing-5 0;
    background: $blue-dark;
    text-align: center;
  }

</style>
