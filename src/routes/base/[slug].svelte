<script context="module">
  // @ts-ignore
  export async function load({ params }) {
    try {
      const BasePost = await import(`../../base-posts/${params.slug}.md`);
      return {
        props: {
          BasePost: BasePost.default,
          tags: BasePost.metadata.tags,
        },
      };
    } catch (e) {
      return {
        status: 404,
        error: "Запись не найдена",
      };
    }
  }
</script>

<script>
  // @ts-nocheck

  export let BasePost;
  export let tags;
</script>

<div class="space-x-3">
  {#each tags as tag}
    <a sveltekit:prefetch href={`/base-tag/${tag}`}>
      {tag}
    </a>
  {/each}
</div>

<div class="mt-4">
  <BasePost />
</div>
