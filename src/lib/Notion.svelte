<script lang="ts">
  import NotionBlock from "./NotionBlock.svelte";

  import "highlight.js/styles/dark.min.css";

  import blocksjson from "./test/blocks.json";
  const blocks = blocksjson.blocks;

  import cdtejson from "./test/cdte.json";
  const codeTest = cdtejson.blocks;

  import chjson from "./test/chzzk.json";
  const chzzk = chjson.blocks;

  let selected = 0;
</script>

<button on:click={() => (selected = 0)}>Notion</button>
<button on:click={() => (selected = 1)}>Code</button>
<button on:click={() => (selected = 2)}>Chzzk</button>

<article class="notion-renderer">
  {#each selected == 0 ? blocks : selected == 1 ? codeTest : chzzk as block}
    <NotionBlock {block} />
  {/each}
</article>

<style>
  .notion-renderer {
    font-size: var(--notion-default-font-size);
    line-height: 1.5;

    flex-shrink: 0;
    flex-grow: 1;
    max-width: 100%;
    display: flex;
    align-items: flex-start;
    flex-direction: column;
    width: 100%;
    z-index: 4;
    padding-bottom: 0px;
    padding-left: 0px;
    padding-right: 0px;

    font-family:
      ui-sans-serif,
      -apple-system,
      BlinkMacSystemFont,
      "Segoe UI Variable Display",
      "Segoe UI",
      Helvetica,
      "Apple Color Emoji",
      Arial,
      sans-serif,
      "Segoe UI Emoji",
      "Segoe UI Symbol";

    max-width: 768px;
    margin: 0 auto;
  }
</style>
