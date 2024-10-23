<script lang="ts">
  import MathMl from "svelte-tex/package/MathML.svelte";
  import DotList from "./components/DotList.svelte";
  import RenderText from "./components/RenderText.svelte";
  import Table from "./components/Table.svelte";
  import Todo from "./components/Todo.svelte";
  import Image from "./components/Image.svelte";
  import Code from "./components/Code.svelte";

  export let block: {
    type: string;
    [key: string]: any;
  };

  const notypecheck = (x: any) => x;
</script>

{#if block.type == "heading_1"}
  <h2 class="notion-heading-1">
    <RenderText block={block["heading_1"]} />
  </h2>
{:else if block.type == "heading_2"}
  <h3 class="notion-heading-2">
    <RenderText block={block["heading_2"]} />
  </h3>
{:else if block.type == "heading_3"}
  <h4 class="notion-heading-3">
    <RenderText block={block["heading_3"]} />
  </h4>
{:else if block.type == "paragraph"}
  <div class="notion-paragraph">
    <RenderText block={block["paragraph"]} />
  </div>
{:else if block.type == "equation"}
  <div class="notion-equation-block">
    <MathMl tex={block.equation.expression} />
  </div>
{:else if block.type == "table"}
  <Table {block} />
{:else if block.type == "image"}
  <Image {block} />
{:else if block.type == "code"}
  <Code {block} />
{:else if block.type == "to_do"}
  {#if block.to_do}
    <Todo block={notypecheck(block)} />
  {/if}
{:else if block.type == "bulleted_list_item"}
  <DotList block={block.bulleted_list_item} />
{:else}
  <details>
    <summary>RAW JSON</summary>
    <pre class="notion-debug">{JSON.stringify(block, null, 2)}</pre>
  </details>
{/if}
