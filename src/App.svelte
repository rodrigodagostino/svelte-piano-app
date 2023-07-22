<script lang="ts">
  import Keys from './lib/Keys.svelte';
  import svelteLogo from './assets/images/svelte-logo.svg';
  import rotateIcon from './assets/images/rotate-solid-icon.svg';
</script>

<main class="app-main">
  <div class="container">
    <p class="orientation-message">
      <img class="orientation-message__icon" src={rotateIcon} alt="" />
      <span class="orientation-message__text">Rotate your screen for a better experience</span>
    </p>
    <Keys />
  </div>
</main>
<footer class="app-footer">
  <div class="container">
    <a href="https://github.com/rodrigodagostino/svelte-piano-app" target="_blank" rel="noreferrer">
      Made with <img src={svelteLogo} alt="Svelte.js logo" /> by Rodrigo D’Agostino
    </a>
  </div>
</footer>

<style lang="scss">
  .container {
    max-width: 54rem;
    margin: 0 auto;
    padding: 1rem;
    position: relative;
  }

  .app-main {
    margin-top: 12vh;
  }

  .orientation-message {
    display: none;
    gap: 0.5rem;
    justify-content: center;
    align-items: center;
    margin-bottom: 3rem;

    &__icon {
      width: auto;
      height: 1rem;
    }
  }

  .app-footer {
    font-size: 0.875rem;
    text-align: center;
    margin-top: auto;

    .container {
      display: flex;
      justify-content: center;
      padding: 1rem 0;
    }

    a {
      color: var(--gray-400);
      text-decoration: none;
      transition: color 0.24s;

      &:focus,
      &:hover {
        color: var(--gray-600);
      }
    }

    img {
      height: 1.25rem;
      width: auto;
      vertical-align: middle;
      margin: 0 0.25rem;
      display: inline-block;
    }
  }

  @media (max-width: 33em) and (orientation: portrait) {
    .orientation-message {
      display: flex;
    }
  }

  @media (min-height: 27.5em) {
    .app-main {
      margin-top: 16vh;
    }
  }

  @media (min-height: 32.5em) {
    .app-main {
      margin-top: 18vh;
    }
  }

  @media (min-height: 43.75em) {
    .app-main {
      margin-top: 24vh;
    }
  }
</style>
