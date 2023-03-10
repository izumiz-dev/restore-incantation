<script>
  import InfoTable from "./lib/InfoTable.svelte";
  import exifr from "exifr";
  let selectedImage, fileinput;
  let imageInfo = {
    height: 0,
    width: 0,
    prompt: "",
    ngPrompt: "",
    steps: 0,
    sampler: "",
    CFGScale: "",
    seed: 0,
    model: "",
  };

  const readExif = async (img) => {
    const parsedInfo = await exifr.parse(img);
    const parameters = parsedInfo.parameters;
    imageInfo.height = parsedInfo.ImageHeight;
    imageInfo.width = parsedInfo.ImageWidth;
    imageInfo.prompt = parameters.match(/^.*(?=\nNegative prompt:)/)[0];
    imageInfo.ngPrompt = parameters.match(
      /(?<=Negative prompt: )(.*?)(?=Steps:)/s
    )[0];
    imageInfo.steps = parameters.match(/(?<=Steps: )(.*?)(?=, Sampler:)/s)[0];
    imageInfo.sampler = parameters.match(
      /(?<=Sampler: )(.*?)(?=, CFG scale:)/s
    )[0];
    imageInfo.CFGScale = parameters.match(
      /(?<=CFG scale: )(.*?)(?=, Seed:)/s
    )[0];
    imageInfo.seed = parameters.match(/(?<=Seed: )(.*?)(?=, )/s)[0];
    imageInfo.model = parameters.match(/(?<=Model: )(.*?)$/s)[0];
  };

  const onFileSelected = (e) => {
    let image = e.target.files[0];
    let reader = new FileReader();
    reader.readAsDataURL(image);
    reader.onload = (e) => {
      selectedImage = e.target.result;
    };
    readExif(image);
  };
</script>

<main />
<div class="description">
  <h2>Restore Incantation</h2>
  <span
    >Stable Diffusionで生成したPNG画像のメタデータから、"呪文"を復活させます。</span
  >
  <a
    href="https://github.com/izumiz-dev/restore-incantation"
    target="_blank"
    rel="noopener noreferrer">Github Repo</a
  >
</div>

<InfoTable {...imageInfo} />

<!-- svelte-ignore a11y-click-events-have-key-events -->
{#if selectedImage}
  <!-- svelte-ignore a11y-missing-attribute -->
  <img class="selectedImage" src={selectedImage} />
{:else}
  <span>No Selected</span>
{/if}
<!-- svelte-ignore a11y-click-events-have-key-events -->
<button
  on:click={() => {
    fileinput.click();
  }}
>
  Select
</button>
<input
  style="display:none"
  type="file"
  accept=".jpg, .jpeg, .png"
  on:change={(e) => onFileSelected(e)}
  bind:this={fileinput}
/>

<style>
  .description {
    margin: auto;
    padding: 1rem;
  }
</style>
