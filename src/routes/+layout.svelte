
<svelte:head>
  <style>
    body {
      margin: 0;
      height: 100vh;
    }
  </style>
</svelte:head>

<main>
  <slot/>
</main>

<style>
  main {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
