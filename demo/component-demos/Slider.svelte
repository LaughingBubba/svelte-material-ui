<section>
  <h2>Slider</h2>

  <div>
    <FormField align="end" style="display: flex;">
      <Slider bind:value />
      <span slot="label" style="padding-right: 12px; width: max-content; display: block;">Amount of Wonder</span>
    </FormField>
  </div>

  <pre class="status">Value: {value}</pre>

  <div>
    Discrete with min/max/step:

    <Slider bind:value={value2} min={-10} max={10} step={2} discrete />
  </div>

  <div>
    Discrete with min/max/step and tick marks:

    <Slider bind:value={value3} min={-10} max={10} step={2} discrete displayMarkers />
  </div>
</section>

<script>
  import Slider from 'svelte-material-ui/components/slider';
  import FormField from 'svelte-material-ui/components/form-field';

  let value = 50;
  let value2 = 0;
  let value3 = 0;
</script>