<script lang="ts">
  import Notion from "./lib/Notion.svelte";

  import blocksjson from "./test/blocks.json";
  const blocks = blocksjson.blocks;

  import cdtejson from "./test/cdte.json";
  const codeTest = cdtejson.blocks;

  import chjson from "./test/chzzk.json";
  const chzzk = chjson.blocks;

  let userInput: any = blocks;
</script>

<button on:click={() => (userInput = blocks)}>Notion</button>
<button on:click={() => (userInput = codeTest)}>Code</button>
<button on:click={() => (userInput = chzzk)}>Chzzk</button>

<div>Hello World</div>

<Notion blocks={userInput} />
