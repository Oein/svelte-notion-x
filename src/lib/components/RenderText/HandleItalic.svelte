<script lang="ts">
  export let annotations: {
    bold: boolean;
    italic: boolean;
    strikethrough: boolean;
    underline: boolean;
    code: boolean;
    color: string;
  };
</script>

{#if annotations.bold}
  <i><slot /></i>
{:else}
  <slot />
{/if}
