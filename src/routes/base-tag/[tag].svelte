<script context="module">
  export async function load({ params }) {
    const posts = await import.meta.globEager("../../base-posts/*.md");
    const postsList = Object.values(posts);
    const postsMeta = postsList.map((post) => {
      return post.metadata;
    });
    const filteredPosts = postsMeta.filter((post) => {
      return post.tags.includes(params.tag);
    });
    if (filteredPosts.length != 0) {
      return {
        props: {
          posts: filteredPosts,
          tagName: String(params.tag),
        },
      };
    } else {
      return {
        status: 404,
        error: "Запись не найдена",
      };
    }
  }
</script>

<script>
  // @ts-nocheck

  export let posts;
  export let tagName;
</script>

<h1>Тег: {tagName}</h1>
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
