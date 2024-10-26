<script lang="ts">
  import DotList from "./components/DotList.svelte";
  import RenderText from "./components/RenderText.svelte";
  import Table from "./components/Table.svelte";
  import Todo from "./components/Todo.svelte";
  import Image from "./components/Image.svelte";
  import Code from "./components/Code.svelte";
  import EquationBlock from "./components/EquationBlock.svelte";
  import DebugJson from "./components/DebugJSON.svelte";
  import Divider from "./components/Divider.svelte";
  import Toggle from "./components/Toggle.svelte";
  import Quote from "./components/Quote.svelte";
  import Callout from "./components/Callout.svelte";
  import NumList from "./components/NumList.svelte";

  export let block: {
    type: string;
    [key: string]: any;
  };

  const notypecheck = (x: any) => x;
</script>

<div class="notion-content">
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
    <EquationBlock block={block.equation} />
  {:else if block.type == "table"}
    <Table block={notypecheck(block)} />
  {:else if block.type == "image"}
    <Image {block} />
  {:else if block.type == "code"}
    <Code {block} />
  {:else if block.type == "divider"}
    <Divider />
  {:else if block.type == "toggle"}
    <Toggle {block} />
  {:else if block.type == "quote"}
    <Quote {block} />
  {:else if block.type == "callout"}
    <Callout {block} />
  {:else if block.type == "to_do"}
    {#if block.to_do}
      <Todo block={notypecheck(block)} />
    {/if}
  {:else if block.type == "bulleted_list_item"}
    <DotList block={notypecheck(block)} />
  {:else if block.type == "numbered_list_item"}
    <NumList
      block={notypecheck(block)}
      number={block.custom && block.custom.number ? block.custom.number : 1}
    />
  {:else}
    <DebugJson {block} name={`Unhandled / ${block.type}`} />
  {/if}
</div>

<style>
  .notion-content {
    width: 100%;
    margin-top: 1px;
    margin-bottom: 1px;
  }
</style>
