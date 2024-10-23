<script lang="ts">
  export let block: {
    [key: string]: any;
  };
  const toNotionImageUrl = (url: string, blockId: string) =>
    `https://notion.so${
      url.startsWith("/image")
        ? url
        : `/image/${encodeURIComponent(url)}?table=block&id=${blockId}`
    }`;
</script>

<img
  src={toNotionImageUrl(block.image.file.url, block.id)}
  alt="image from notion"
/>

<!-- <details>
  <summary>RAW JSON: IMAGE</summary>
  <pre class="notion-debug">{JSON.stringify(block, null, 2)}</pre>
</details> -->
