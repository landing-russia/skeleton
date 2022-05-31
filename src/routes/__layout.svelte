<script context="module">
  export const load = async ({ url }) => ({
    props: {
      url,
    },
  });
</script>

<script>
// @ts-nocheck

  import "../app.css";
  import Footer from "$lib/layout/Footer.svelte";
  import Nav from "$lib/layout/Nav.svelte";
  import PageTransition from "$lib/PageTransition.svelte";
  export let url;
</script>

<Nav />

<main class="pt-16 flex-grow w-full">
  <PageTransition {url}>
    <slot />
  </PageTransition>
</main>

<Footer />
