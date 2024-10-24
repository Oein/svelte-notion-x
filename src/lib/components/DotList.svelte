<script lang="ts">
  import Notion from "../Notion.svelte";
  import NotionBlock from "../NotionBlock.svelte";
  import DebugJson from "./DebugJSON.svelte";
  import RenderText from "./RenderText.svelte";

  export let block: {
    [key: string]: any;
    bulleted_list_item: {
      rich_text: any;
    };
    children: any[];
  };
</script>

<div class="notion-list">
  <div class="notion-list-dot">
    <div class="notion-list-dot-inner"></div>
  </div>
  <div class="notion-list-content">
    <RenderText block={block.bulleted_list_item} />
    {#if block.children}
      {#each block.children as blc}
        <NotionBlock block={blc} />
      {/each}
    {/if}
  </div>
</div>

<!-- <DebugJson {block} name="dot-list" /> -->

<style>
  .notion-list {
    display: flex;
    align-items: flex-start;
    width: 100%;
    padding-left: 2px;
    color: inherit;
    fill: inherit;
  }
  .notion-list-dot {
    user-select: none;
    --pseudoSelection--background: transparent;
    margin-right: 2px;
    width: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-grow: 0;
    flex-shrink: 0;
    min-height: calc(1.5em + 6px);
  }
  .notion-list-dot-inner {
    font-size: 1.5em;
    line-height: 1;
    margin-bottom: 0px;
    --pseudoBefore--fontFamily: Arial;
    --pseudoBefore--content: "•";
  }
  .notion-list-dot-inner:before {
    background: var(--pseudoBefore--background);
    border: var(--pseudoBefore--border);
    color: var(--pseudoBefore--color);
    content: var(--pseudoBefore--content);
    display: var(--pseudoBefore--display) !important;
    font-family: var(--pseudoBefore--fontFamily);
    font-size: var(--pseudoBefore--fontSize);
    font-weight: var(--pseudoBefore--fontWeight);
    height: var(--pseudoBefore--height);
    width: var(--pseudoBefore--width);
  }
</style>
