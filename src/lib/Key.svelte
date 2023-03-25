<script lang="ts" context="module">
  export interface IKey {
    note:
      | 'c'
      | 'c-sharp'
      | 'd'
      | 'd-sharp'
      | 'e'
      | 'e-sharp'
      | 'f'
      | 'f-sharp'
      | 'g'
      | 'g-sharp'
      | 'a'
      | 'a-sharp'
      | 'b'
    type: 'white' | 'black'
    key: 'a' | 'w' | 's' | 'e' | 'd' | 'f' | 't' | 'g' | 'y' | 'h' | 'u' | 'j'
  }
</script>

<script lang="ts">
  export let note: IKey['note']
  export let type: IKey['type']
  export let key: IKey['key']

  const handleOnClick = (_: MouseEvent, note: IKey['note']) => {
    const audio = new Audio(`./assets/sounds/${note}.mp3`)
    audio.play()
  }
</script>

<button class={`key key--${type}`} on:click={(event) => handleOnClick(event, note)}>
  {key.toUpperCase()}
</button>

<style lang="scss">
  .key {
    --white-key-width: 4rem;
    display: flex;
    justify-content: center;
    align-items: end;
    padding: 1rem 0;
    border: none;

    &--white {
      width: var(--white-key-width);
      background-color: var(--white);
      z-index: 0;

      &:focus {
        z-index: 1;
      }
    }

    &--black {
      width: calc(var(--white-key-width) / 2);
      height: 60%;
      margin: 0 calc(var(--white-key-width) / 4 * -1);
      background-color: var(--black);
      color: var(--white);
      z-index: 10;
    }
  }
</style>
