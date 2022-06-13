<script context="module">
  export async function load() {
    const posts = await import.meta.globEager("../../base-posts/*.md");
    const postsList = Object.values(posts);
    const postsMeta = postsList.map((post) => {
      return post.metadata;
    });
    console.log(postsMeta);
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
    </div>
  </a>
{/each}
