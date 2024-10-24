<script lang="ts">
  import DebugJson from "./DebugJSON.svelte";

  export let block: {
    [key: string]: any;
  };
</script>

<DebugJson {block} name="table" />
