<tbody
  use:useActions={use}
  use:forwardEvents
  class="mdc-data-table__content {className}"
  {...exclude($$props, ['use', 'class'])}
><slot></slot></tbody>

<script>
  import {setContext} from 'svelte';
  import {current_component} from 'svelte/internal';
  import {forwardEventsBuilder} from '../forwardEvents.js';
  import {exclude} from '../exclude.js';
  import {useActions} from '../useActions.js';

  const forwardEvents = forwardEventsBuilder(current_component);

  export let use = [];
  let className = '';
  export {className as class};

  setContext('SMUI:data-table:row:header', false);
</script>