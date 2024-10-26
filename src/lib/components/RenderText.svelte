<script lang="ts">
  import HandleAnnotation from "./RenderText/HandleAnnotation.svelte";
  import MathML from "svelte-tex/package/MathML.svelte";

  export let block: {
    rich_text: {
      plain_text: string;
      type: string;
      text: {
        content: string;
        link: string | null;
      };
      annotations: {
        bold: boolean;
        italic: boolean;
        strikethrough: boolean;
        underline: boolean;
        code: boolean;
        color: string;
      };
      [key: string]: any;
    }[];
    [key: string]: any;
  };
</script>

{#each block.rich_text as text, i}
  {#if text.type == "text"}
    <HandleAnnotation
      lastAnnotations={block.rich_text[i - 1]?.annotations}
      nextAnnotations={block.rich_text[i + 1]?.annotations}
      annotations={text.annotations}
      text={text.text.content}
    />
  {:else if text.type == "equation"}
    <MathML tex={text.equation.expression} />
  {:else}
    <span class="notion-render">{text.plain_text}</span>
  {/if}
{/each}

<!-- <details>
  <summary>RAW JSON: RichText</summary>
  <pre class="notion-debug">{JSON.stringify(block, null, 2)}</pre>
</details> -->
