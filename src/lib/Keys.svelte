<script lang="ts">
  import Key, { type IKey } from './Key.svelte'

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
  ]

  const handleOnKeydown = (event) => {
    const filteredKey = keys.filter((key) => key.key === event.key.toLowerCase())[0]
    filteredKey && new Audio(`./assets/sounds/${filteredKey.note}.mp3`).play()
  }
</script>

<svelte:window on:keydown={handleOnKeydown} />

<div class="keys">
  {#each keys as { note, type, key }}
    <Key {note} {type} {key} />
  {/each}
</div>

<style lang="scss">
  .keys {
    display: flex;
    height: 20rem;
  }
</style>
