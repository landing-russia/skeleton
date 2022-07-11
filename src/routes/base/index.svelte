<script context="module">
  export async function load() {
    const posts = await import.meta.globEager("../../base-posts/*.md");
    const postsList = Object.values(posts);
    const postsMeta = postsList
      .map((post) => {
        return post.metadata;
      })
      .sort((a, b) => (a.date < b.date ? 1 : -1));
    return {
      props: {
        posts: postsMeta,
      },
    };
  }
</script>

<script>
  // @ts-nocheck

  export let posts;
</script>

<h1>База</h1>
{#each posts as post}
  <a sveltekit:prefetch href={`/base/${post.slug}`}>
    <div class="shadow rounded-lg p-4 bg-white mt-4">
      <div class="space-x-3">
        {#each post.tags as tag}
          <a sveltekit:prefetch href={`/base-tag/${tag}`}>
            {tag}
          </a>
        {/each}
      </div>
      <h2 class="my-0">{post.title}</h2>
      <span class="mt-3 text-sm">{new Date(post.date).toLocaleDateString('ru-RU', {
        year: "numeric",
        month: "long",
        day: "numeric"
      })}</span>
    </div>
  </a>
{/each}
