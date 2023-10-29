<script lang="ts">
  import Key, { type IKey } from './Key.svelte';

  export const keys: IKey[] = [
    {
      note: 'c',
      type: 'white',
      key: 'a',
    },
    {
      note: 'c-sharp',
      type: 'black',
      key: 'w',
    },
    {
      note: 'd',
      type: 'white',
      key: 's',
    },
    {
      note: 'd-sharp',
      type: 'black',
      key: 'e',
    },
    {
      note: 'e',
      type: 'white',
      key: 'd',
    },
    {
      note: 'f',
      type: 'white',
      key: 'f',
    },
    {
      note: 'f-sharp',
      type: 'black',
      key: 't',
    },
    {
      note: 'g',
      type: 'white',
      key: 'g',
    },
    {
      note: 'g-sharp',
      type: 'black',
      key: 'y',
    },
    {
      note: 'a',
      type: 'white',
      key: 'h',
    },
    {
      note: 'a-sharp',
      type: 'black',
      key: 'u',
    },
    {
      note: 'b',
      type: 'white',
      key: 'j',
    },
  ];

  let activeKeys: string[] = [];

  const handleOnKeyDown = (event: KeyboardEvent) => {
    const filteredKey = keys.filter((key) => key.key === event.key.toLowerCase())[0];
    if (filteredKey && !activeKeys.includes(filteredKey.key)) {
      activeKeys = [...activeKeys, event.key.toLowerCase()];
      new Audio(`./assets/sounds/${filteredKey.note}.mp3`).play();
    }
  };

  const handleOnKeyUp = (event: KeyboardEvent) => {
    const filteredKey = keys.filter((key) => key.key === event.key.toLowerCase())[0];
    if (filteredKey) {
      activeKeys = activeKeys.filter((activeKey) => activeKey !== event.key.toLowerCase());
    }
  };
</script>

<svelte:window on:keydown={handleOnKeyDown} on:keyup={handleOnKeyUp} />

<div class="keys">
  {#each keys as { note, type, key }}
    <Key {note} {type} {key} isActive={activeKeys.includes(key)} />
  {/each}
</div>

<audio src="./assets/sounds/a.mp3" preload="auto" />
<audio src="./assets/sounds/a-sharp.mp3" preload="auto" />
<audio src="./assets/sounds/b.mp3" preload="auto" />
<audio src="./assets/sounds/c.mp3" preload="auto" />
<audio src="./assets/sounds/c-sharp.mp3" preload="auto" />
<audio src="./assets/sounds/d.mp3" preload="auto" />
<audio src="./assets/sounds/d-sharp.mp3" preload="auto" />
<audio src="./assets/sounds/e.mp3" preload="auto" />
<audio src="./assets/sounds/f.mp3" preload="auto" />
<audio src="./assets/sounds/f-sharp.mp3" preload="auto" />
<audio src="./assets/sounds/g.mp3" preload="auto" />
<audio src="./assets/sounds/g-sharp.mp3" preload="auto" />

<style lang="scss">
  .keys {
    --keys-gap: 0.5rem;
    display: flex;
    gap: var(--keys-gap);
    height: 14rem;
  }

  @media (min-height: 27.5em) {
    .keys {
      height: 16rem;
    }
  }

  @media (min-height: 32.5em) {
    .keys {
      height: 18rem;
    }
  }

  @media (min-height: 43.75em) {
    .keys {
      height: 20rem;
    }
  }
</style>
