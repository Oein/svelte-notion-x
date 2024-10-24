<script lang="ts">
  import DebugJson from "./DebugJSON.svelte";
  import RenderText from "./RenderText.svelte";

  export let block: {
    [key: string]: any;
    to_do: {
      checked: boolean;
      rich_text: any;
    };
  };
</script>

<div class="notion-todo">
  <div>
    <input
      class="notion-todo-checkbox"
      type="checkbox"
      checked={block.to_do.checked}
    />
  </div>
  <div>
    <RenderText block={block.to_do} />
  </div>
</div>

<!-- <DebugJson {block} name="todo" /> -->
