<script>
  export let undoManager;

  import { undo } from 'svelt-yjs';

  import ImageButton from './ImageButton.svelte';

  import undoIcon from './images/undo.png';
  import redoIcon from './images/redo.png';

  const undoStore = undo.readable(undoManager);
</script>

<style>
  panel {
    position: fixed;
    bottom: 0;
    left: 50%;
    transform: translate(-50%);

    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;

    padding: 8px;
    background-color: var(--light);
  }
</style>

<panel>
  <ImageButton
    disabled={$undoStore.undoSize === 0}
    icon={undoIcon}
    on:click={() => undoManager.undo()}>
    Undo
    {#if $undoStore.undoSize > 0}({$undoStore.undoSize}){/if}
  </ImageButton>
  <ImageButton
    disabled={$undoStore.redoSize === 0}
    icon={redoIcon}
    on:click={() => undoManager.redo()}>
    Redo
    {#if $undoStore.redoSize > 0}({$undoStore.redoSize}){/if}
  </ImageButton>
</panel>
