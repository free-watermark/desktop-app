
<input
  hidden
  type="file"
  id="file-drop-zone"
  accept=".png,.jpg,.jpeg" 
  on:change={setSelectedFileAndPreview}
/>
<label
  for="file-drop-zone"
  id="file-drop-zone-box"
  on:dragover|preventDefault
  on:drop|preventDefault={setDroppedFileAndPreview}
>
  {#if fileObjectUrl}
    <img
      src={fileObjectUrl}
      class="watermarking-preview"
      alt="file-in-watermark-editing"
    />
  {:else}
    <p>click to select or drag and drop your file here</p>
  {/if}
</label>

<script lang="ts">
  let currentFile: File;
  let fileObjectUrl: string;

  const setSelectedFileAndPreview = (event: Event & { currentTarget: EventTarget & HTMLInputElement }) => {
    if (event.currentTarget.files?.length) {
      currentFile = event.currentTarget.files[0];
      fileObjectUrl = URL.createObjectURL(currentFile);
    }
  };

  const setDroppedFileAndPreview = (event: DragEvent & { currentTarget: EventTarget & HTMLLabelElement; }) => {
    if (event.dataTransfer?.files) {
      currentFile = event.dataTransfer.files[0];
      fileObjectUrl = URL.createObjectURL(currentFile);
    }
  };
</script>

<style>
  #file-drop-zone-box {
    width: 50%;
    z-index: 8;
    height: 40%;
    padding: 8px;
    display: flex;
    cursor: pointer;
    transition: .32s;
    border-radius: 4px;
    align-items: center;
    justify-content: center;
    border: 4px solid darkmagenta;
  }

  .watermarking-preview {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
</style>
