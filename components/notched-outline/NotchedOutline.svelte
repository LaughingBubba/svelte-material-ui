<div
  bind:this={element}
  use:useActions={use}
  use:forwardEvents
  class="mdc-notched-outline {className}"
  class:mdc-notched-outline--notched={notched}
  class:mdc-notched-outline--no-label={noLabel}
  {...exclude($$props, ['use', 'class', 'notched', 'noLabel'])}
>
  <div class="mdc-notched-outline__leading"></div>
  {#if !noLabel}
    <div class="mdc-notched-outline__notch"><slot></slot></div>
  {/if}
  <div class="mdc-notched-outline__trailing"></div>
</div>

<script>
  import {MDCNotchedOutline} from '@material/notched-outline';
  import {onMount, onDestroy} from 'svelte';
  import {current_component} from 'svelte/internal';
  import {forwardEventsBuilder} from '../forwardEvents.js';
  import {exclude} from '../exclude.js';
  import {useActions} from '../useActions.js';

  const forwardEvents = forwardEventsBuilder(current_component);

  export let use = [];
  let className = '';
  export {className as class};
  export let notched = false;
  export let noLabel = false;

  let element;
  let notchedOutline;

  onMount(() => {
    notchedOutline = new MDCNotchedOutline(element);
  });

  onDestroy(() => {
    notchedOutline.destroy();
  });

  export function notch(notchWidth, ...args) {
    return notchedOutline.notch(notchWidth, ...args);
  }

  export function closeNotch(...args) {
    return notchedOutline.closeNotch(...args);
  }
</script>