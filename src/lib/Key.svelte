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
    isActive?: boolean
  }
</script>

<script lang="ts">
  export let note: IKey['note']
  export let type: IKey['type']
  export let key: IKey['key']
  export let isActive = false

  const handleOnKeyDown = (event: KeyboardEvent, note: IKey['note']) => {
    if (event.code === 'Enter' || event.code === 'Space') {
      isActive = true
      const audio = new Audio(`./assets/sounds/${note}.mp3`)
      audio.play()
    }
  }

  const handleOnMouseDown = (note: IKey['note']) => {
    isActive = true
    const audio = new Audio(`./assets/sounds/${note}.mp3`)
    audio.play()
  }

  const handleOnKeyOrMouseUp = () => (isActive = false)
</script>

<button
  class={`key key--${type}`}
  class:is-active={isActive}
  on:keydown={(event) => handleOnKeyDown(event, note)}
  on:keyup={handleOnKeyOrMouseUp}
  on:mousedown={() => handleOnMouseDown(note)}
  on:mouseup={handleOnKeyOrMouseUp}
>
  <span class="key__letter">{key.toUpperCase()}</span>
</button>

<style lang="scss">
  .key {
    --white-key-width: 4rem;
    --black-key-width: calc(var(--white-key-width) / 8 * 5);
    --key-border-radius: 0.375rem;
    display: flex;
    justify-content: center;
    align-items: end;
    padding: 1rem 0;
    border: none;
    border-radius: var(--key-border-radius);
    outline: 0.1875rem solid transparent;
    transform: translate3d(0, 0, 0);
    transition: background-color 0.24s ease, box-shadow 0.24s ease, transform 0.24s ease,
      outline 0.24s;
    will-change: box-shadow, transform;
    cursor: pointer;

    &__letter {
      color: inherit;
      z-index: 1;
    }

    &::before {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(
        100% 100% at 100% 0%,
        rgba(255, 255, 255, 0.75) 0%,
        rgba(0, 0, 0, 0) 100%
      );
      border-radius: var(--key-border-radius);
      mix-blend-mode: overlay;
    }

    &:focus-visible {
      outline-color: var(--cyan-500);
    }

    &--white {
      --box-shadow-height: 1rem;
      --box-shadow-height--pressed: 0.25rem;
      width: var(--white-key-width);
      background: var(--gray-050);
      box-shadow: 0 var(--box-shadow-height) 0 var(--gray-200),
        0 -0.0625rem 0.25rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 0.125rem) 0.125rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 0.25rem) 0.25rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 0.5rem) 0.5rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 1rem) 1rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 2rem) 2rem rgba(45, 35, 66, 0.12);
      color: var(--gray-800);
      text-shadow: 0 1px 1px rgba(45, 35, 66, 0.16);

      &.is-active {
        background: var(--cyan-100);
        box-shadow: 0 var(--box-shadow-height--pressed) 0 var(--cyan-300),
          0 -0.0625rem 0.25rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.0625rem) 0.0625rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.1875rem) 0.125rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.25rem) 0.25rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.375rem) 0.5rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.875rem) 1rem rgba(45, 35, 66, 0.12);
        transform: translate3d(
          0,
          calc(var(--box-shadow-height) - var(--box-shadow-height--pressed)),
          0
        );
      }
    }

    &--black {
      --box-shadow-height: 0.75rem;
      --box-shadow-height--pressed: 0.25rem;
      width: var(--black-key-width);
      height: 60%;
      margin: -1.5rem calc((var(--black-key-width) / 2 + var(--keys-gap) / 2) * -1) 0;
      background: var(--gray-700);
      box-shadow: 0 var(--box-shadow-height) 0 var(--gray-800),
        0 -0.0625rem 0.25rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 0.125rem) 0.125rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 0.25rem) 0.25rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 0.5rem) 0.5rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 1rem) 1rem rgba(45, 35, 66, 0.12),
        0 calc(var(--box-shadow-height) + 2rem) 2rem rgba(45, 35, 66, 0.12);
      color: var(--gray-050);
      text-shadow: 0 1px 1px rgba(45, 35, 66, 0.32);
      z-index: 10;

      &.is-active {
        background-color: var(--cyan-700);
        box-shadow: 0 var(--box-shadow-height--pressed) 0 var(--cyan-800),
          0 -0.0625rem 0.25rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.0625rem) 0.0625rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.1875rem) 0.125rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.25rem) 0.25rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.375rem) 0.5rem rgba(45, 35, 66, 0.12),
          0 calc(var(--box-shadow-height--pressed) + 0.875rem) 1rem rgba(45, 35, 66, 0.12);
        transform: translate3d(
          0,
          calc(var(--box-shadow-height) - var(--box-shadow-height--pressed)),
          0
        );
      }
    }
  }
</style>
