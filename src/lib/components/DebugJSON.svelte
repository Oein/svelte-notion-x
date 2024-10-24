<script lang="ts">
  export let block: any;
  export let name: string;
</script>

<details>
  <summary>{name}</summary>
  <pre class="notion-debug">{JSON.stringify(block, null, 2)}</pre>
</details>
