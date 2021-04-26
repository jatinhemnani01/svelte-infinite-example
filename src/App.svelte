<script>
  import { onMount } from "svelte";
  import InfiniteScroll from "./InfiniteScroll.svelte";
  let posts = [];
  async function getPosts() {
    let res = await fetch("https://meme-api.herokuapp.com/gimme/10");
    let data = await res.json();
    posts = [...posts, ...data.memes];
    console.log(posts);
  }
  onMount(() => {
    getPosts();
  });
</script>

{#each posts as item}
  <h1 style="padding:1em">{item.title}</h1>
{/each}

<InfiniteScroll on:scroll={getPosts} />
