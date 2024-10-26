<script lang="ts">
  import hljs from "highlight.js";
  import { onMount } from "svelte";
  import mermaid from "mermaid";

  let container: HTMLSpanElement;

  export let block: {
    [key: string]: any;
  };

  let preElement: HTMLElement;
  onMount(async () => {
    if (block.code.language == "mermaid") {
      const { svg } = await mermaid.render(
        "mermaid",
        block.code.rich_text[0].text.content
      );
      container.innerHTML = svg;
      return;
    }
    hljs.highlightBlock(preElement.children[0] as any);
  });
</script>

{#if block.code.language == "mermaid"}
  <div bind:this={container} class="notion-mermaid-container"></div>
{:else}
  <pre
    bind:this={preElement}>{@html `<code>${block.code.rich_text[0].text.content}</code>`}</pre>
{/if}

<!-- <details>
  <summary>RAW JSON: CODE</summary>
  <pre class="notion-debug">{JSON.stringify(block, null, 2)}</pre>
</details> -->

<style>
  .notion-mermaid-container {
    background: #f7f6f3;
    max-width: 100%;
    overflow: auto;
    display: flex;
    justify-content: center;
  }
</style>
