<i
  bind:this={element}
  use:useActions={use}
  use:forwardEvents
  class="mdc-text-field__icon {className}"
  {tabindex}
  aria-hidden={tabindex === '-1' ? 'true' : 'false'}
  {...exclude($$props, ['use', 'class', 'tabindex'])}
><slot></slot></i>

<script>
  import {MDCTextFieldIcon} from '@material/textfield/icon';
  import {onMount, onDestroy} from 'svelte';
  import {current_component} from 'svelte/internal';
  import {forwardEventsBuilder} from '../../forwardEvents.js';
  import {exclude} from '../../exclude.js';
  import {useActions} from '../../useActions.js';

  const forwardEvents = forwardEventsBuilder(current_component);

  export let use = [];
  let className = '';
  export {className as class};
  export let role = undefined; // Intentionally left out of exclude call above.
  export let tabindex = role !== undefined ? '0' : '-1';

  let element;
  let icon;

  onMount(() => {
    icon = new MDCTextFieldIcon(element);
  });

  onDestroy(() => {
    icon.destroy();
  });
</script>