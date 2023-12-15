<script>
  import Header from './Header.svelte';
  import '../app.css';
</script>

<div class="flex justify-center w-full">
  <div class="flex flex-col">
    <Header />
    <main>
      <slot />
    </main>
  </div>
</div>