<section
  use:useActions={use}
  use:forwardEvents
  class="mdc-top-app-bar__section {className}"
  class:mdc-top-app-bar__section--align-start={align === 'start'}
  class:mdc-top-app-bar__section--align-end={align === 'end'}
  {...roleProp}
  {...exclude($$props, ['use', 'class', 'align', 'toolbar'])}
><slot></slot></section>

<script>
  import {setContext} from 'svelte';
  import {current_component} from 'svelte/internal';
  import {forwardEventsBuilder} from '../forwardEvents.js';
  import {exclude} from '../exclude.js';
  import {useActions} from '../useActions.js';

  const forwardEvents = forwardEventsBuilder(current_component, ['MDCList:action']);

  export let use = [];
  let className = '';
  export {className as class};
  export let align = 'start';
  export let toolbar = false;

  $: roleProp = toolbar ? {role: 'toolbar'} : {};

  setContext('SMUI:icon-button:context', toolbar ? 'top-app-bar:action' : 'top-app-bar:navigation');
  setContext('SMUI:button:context', toolbar ? 'top-app-bar:action' : 'top-app-bar:navigation');
</script>