<div
  use:useActions={line$use}
  class="mdc-text-field-helper-line {line$class}"
  {...exclude(prefixFilter($$props, 'line$'), ['use', 'class'])}
>
  <div
    bind:this={element}
    use:useActions={use}
    use:forwardEvents
    class="mdc-text-field-helper-text {className}"
    class:mdc-text-field-helper-text--persistent={persistent}
    class:mdc-text-field-helper-text--validation-msg={validationMsg}
    aria-hidden="true"
    {...exclude($$props, ['use', 'class', 'persistent', 'validationMsg'])}
  ><slot></slot></div>
  <slot name="character-counter"></slot>
</div>

<script>
  import {MDCTextFieldHelperText} from '@material/textfield/helper-text';
  import {onMount, onDestroy} from 'svelte';
  import {current_component} from 'svelte/internal';
  import {forwardEventsBuilder} from '../../forwardEvents.js';
  import {exclude} from '../../exclude.js';
  import {prefixFilter} from '../../prefixFilter.js';
  import {useActions} from '../../useActions.js';

  const forwardEvents = forwardEventsBuilder(current_component);

  export let use = [];
  let className = '';
  export {className as class};
  export let persistent = false;
  export let validationMsg = false;
  export let line$use = [];
  export let line$class = '';

  let element;
  let helperText;

  onMount(() => {
    helperText = new MDCTextFieldHelperText(element);
  });

  onDestroy(() => {
    helperText.destroy();
  });
</script>