<textarea
  bind:this={element}
  use:useActions={use}
  use:forwardEvents
  class="mdc-text-field__input {className}"
  bind:value
  on:change={changeHandler}
  {...exclude($$props, ['use', 'class', 'value', 'dirty', 'invalid', 'updateInvalid'])}
/>

<script>
  import {onMount} from 'svelte';
  import {current_component} from 'svelte/internal';
  import {forwardEventsBuilder} from '../forwardEvents.js';
  import {exclude} from '../exclude.js';
  import {useActions} from '../useActions.js';

  const forwardEvents = forwardEventsBuilder(current_component, ['change', 'input']);

  export let use = [];
  let className = '';
  export {className as class};
  export let value = '';
  export let dirty = false;
  export let invalid = false;
  export let updateInvalid = true;

  let element;

  onMount(() => {
    if (updateInvalid) {
      invalid = element.matches(':invalid');
    }
  });

  function changeHandler() {
    dirty = true;
    if (updateInvalid) {
      invalid = element.matches(':invalid');
    }
  }
</script>