<script lang="ts">
  let {children} = $props()
</script>

<div class="container-outer">
  <div class="container-inner">
    {@render children()}
  </div>
</div>

<style>
  .container-outer {
    display: flex;
    flex-direction: row;
    width: 100%;
    justify-content: center;

    .container-inner {
      width: 100%;
      max-width: 60rem;
    }
  }
</style>
