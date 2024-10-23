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

{#each block.rich_text as text}
  {#if text.type == "text"}
    <span
      class={`notion-rich-text`}
      style={`${(() => {
        if (text.annotations.color.includes("_background")) {
          return `background-color: var(--notion-back-${text.annotations.color.replace("_background", "")});`;
        }
        return `color: var(--notion-fore-${text.annotations.color});`;
      })()}`}
    >
      <HandleAnnotation
        annotations={text.annotations}
        text={text.text.content}
      />
    </span>
  {:else if text.type == "equation"}
    <MathML tex={text.equation.expression} />
  {:else}
    <span>{text.plain_text}</span>
  {/if}
{/each}

<!-- <details>
  <summary>RAW JSON: RichText</summary>
  <pre class="notion-debug">{JSON.stringify(block, null, 2)}</pre>
</details> -->
