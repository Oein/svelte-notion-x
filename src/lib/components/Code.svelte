<script lang="ts">
  import hljs from "highlight.js";
  import { onMount } from "svelte";
  export let block: {
    [key: string]: any;
  };

  let preElement: HTMLElement;
  onMount(() => {
    // hljs.highlightBlock(codeElement);
    hljs.highlightBlock(preElement.children[0] as any);
  });
</script>

<pre
  bind:this={preElement}>{@html `<code>${block.code.rich_text[0].text.content}</code>`}</pre>

<details>
  <summary>RAW JSON: CODE</summary>
  <pre class="notion-debug">{JSON.stringify(block, null, 2)}</pre>
</details>
