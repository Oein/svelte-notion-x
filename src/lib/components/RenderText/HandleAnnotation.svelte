<script lang="ts">
  export let annotations: {
    bold: boolean;
    italic: boolean;
    strikethrough: boolean;
    underline: boolean;
    code: boolean;
    color: string;
  };
  export let text: string;

  let tags: string[] = [];
  let htmlTAGS: string = "";
  let htmlENDER: string = "";

  $: (() => {
    tags = [];
    if (annotations.bold) tags.push("b");
    if (annotations.italic) tags.push("i");
    if (annotations.strikethrough) tags.push("s");
    if (annotations.underline) tags.push("u");
    for (let tag of tags) {
      htmlTAGS += `<${tag}>`;
      htmlENDER = `</${tag}>` + htmlENDER;
    }
  })();
</script>

{@html htmlTAGS + text + htmlENDER}
