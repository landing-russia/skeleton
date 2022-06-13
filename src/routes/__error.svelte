<script context="module">
  export function load({ error, status }) {
    return {
      props: {
        error,
        status,
      },
    };
  }
</script>

<script>
// @ts-nocheck

  export let status;
  export let error;
</script>

<div class="prose max-w-prose mx-auto pt-16">
  <h1>ОШИБКА!</h1>

  <h3>{status}</h3>
  <h3>{error.message}</h3>
</div>
