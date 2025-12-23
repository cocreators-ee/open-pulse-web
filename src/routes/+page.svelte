<script lang="ts">
  import Container from "$lib/Container.svelte";
  import {onDestroy, onMount} from "svelte";
  import {fly} from "svelte/transition";

  import GooglePlay from "$lib/assets/GetItOnGooglePlay_Badge_Web_color_English.svg?component"

  const images = [
    "/phoneScreenshots/1_en-US.png",
    "/phoneScreenshots/2_en-US.png",
    "/phoneScreenshots/3_en-US.png",
    "/phoneScreenshots/4_en-US.png",
    "/phoneScreenshots/5_en-US.png",
  ]

  const IMAGE_DELAY = 5_000

  let imageIdx = $state(0)
  let imageInterval: number | undefined = undefined

  function nextImage() {
    imageIdx = (imageIdx + 1) % images.length
  }

  onMount(() => {
    imageInterval = setInterval(nextImage, IMAGE_DELAY)
  })

  onDestroy(() => {
    if (imageInterval) {
      clearInterval(imageInterval)
    }
  })
</script>

<svelte:head>
  {#each images as image}
    <link rel="preload" as="image" href={image} fetchpriority="high">
  {/each}
</svelte:head>

<h1>Open Pulse</h1>

<div class="hero-wrapper">
  <Container>
    <div class="hero">
      <div class="left">
        <h2>Open Pulse: Bluetooth LE heart rate monitor</h2>
        <p>Stay in sync with your pulse wherever you want, Open Pulse connects instantly to any BLE‑compatible
          heart rate strap or watch and shows you real‑time data at a glance.</p>
        <p>Built with ❤️ from Estonia: Built by Cocreators OÜ, a small Estonian company focused on quality
          software. You'll be protected by GDPR regardless of where you are.</p>
        <p>No subscriptions, no nonsense: No need to accept Terms of Service, no signups, no payment required.
          Just install and connect to your device.</p>
        <div class="download">
          <a href="https://play.google.com/store/apps/details?id=ee.cocreators.hrapp" target="_blank"
             rel="noopener">
            <GooglePlay alt="Get it on Google Play"/>
          </a>
        </div>
      </div>
      <div class="right">
        {#each images as image, idx}
          {#if imageIdx === idx}
            <img src={image} transition:fly={{x: 100}}/>
          {/if}
        {/each}
      </div>
    </div>
  </Container>
</div>

<section>
  <Container>
    <div class="video-section">
      <h2>Watch video</h2>
      <div class="video">
        <iframe width="288" height="500" src="https://www.youtube.com/embed/8z4nbk7CLNs?si=zhd-_kTWRhlKBtS7"
                title="YouTube video player" frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
      </div>
    </div>
  </Container>
</section>

<style lang="scss">
  @use "variables" as *;

  h1, h2 {
    margin: $spacing-5 0 $spacing-6 0;
    text-align: center;
  }

  .hero-wrapper {
    background: $blue-vibrant;

    .hero {
      min-height: 300px;
      display: flex;
      flex-direction: row;
      align-items: center;
      gap: $spacing-5;
      padding: $spacing-5 0;

      .left {
        display: flex;
        flex-direction: column;

        h2 {
          margin: 0 0 $spacing-2 0;
        }

        .download {
          padding: $spacing-4;
          text-align: center;

          :global(svg) {
            height: 4rem;
          }
        }
      }

      .right {
        position: relative;
        min-height: 500px;
        min-width: 288px;

        img {
          position: absolute;
          left: 0;
          height: 500px;
          max-height: 500px;
        }
      }

      @include mobile {
        flex-direction: column;
      }
    }
  }

  section {
    margin: $spacing-4 0 $spacing-8 0;
  }

  .video-section {
    display: flex;
    flex-direction: column;

    .video {
      align-self: center;
    }
  }
</style>
