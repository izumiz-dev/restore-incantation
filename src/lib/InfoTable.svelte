<script>
  export let height;
  export let width;
  export let prompt;
  export let ngPrompt;
  export let steps;
  export let sampler;
  export let CFGScale;
  export let seed;
  export let model;
</script>

<div class="infoTable">
  <table>
    <tbody>
      <tr>
        <td>Width</td>
        <td>{height || ""}</td>
      </tr>
      <tr>
        <td>Height</td>
        <td>{width || ""}</td>
      </tr>
      <tr>
        <td>Prompt</td>
        <td>{prompt || ""}</td>
      </tr>
      <tr>
        <td>NegativePrompt</td>
        <td>{ngPrompt || ""}</td>
      </tr>
      <tr>
        <td>Steps</td>
        <td>{steps || ""}</td>
      </tr>
      <tr>
        <td>Sampler</td>
        <td>{sampler || ""}</td>
      </tr>
      <tr>
        <td>CFG Scale</td>
        <td>{CFGScale || ""}</td>
      </tr>
      <tr>
        <td>Seed</td>
        <td>{seed || ""}</td>
      </tr>
      <tr>
        <td>Model</td>
        <td>{model || ""}</td>
      </tr>
    </tbody>
  </table>
</div>

<style>
  table {
    border: 1px solid #aaa;
    border-collapse: collapse;
    border-spacing: 0;
    border-radius: 6px;
  }
  table td {
    padding: 0.5em 2em;
    border: 1px solid #aaa;
  }
  .infoTable {
    margin: auto;
    padding: 1rem;
  }
</style>
