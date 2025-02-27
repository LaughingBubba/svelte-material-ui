<aside
  bind:this={element}
  use:useActions={use}
  use:forwardEvents
  class="mdc-drawer {className}"
  class:mdc-drawer--dismissible={variant === 'dismissible'}
  class:mdc-drawer--modal={variant === 'modal'}
  on:MDCDrawer:opened={updateOpen} on:MDCDrawer:closed={updateOpen}
  {...exclude($$props, ['use', 'class', 'variant', 'open'])}
><slot></slot></aside>

<script>
  import {MDCDrawer} from "@material/drawer";
  import {onMount, onDestroy, afterUpdate, setContext} from 'svelte';
  import {current_component} from 'svelte/internal';
  import {forwardEventsBuilder} from '../forwardEvents.js';
  import {exclude} from '../exclude.js';
  import {useActions} from '../useActions.js';

  const forwardEvents = forwardEventsBuilder(current_component, ['MDCDrawer:opened', 'MDCDrawer:closed']);

  export let use = [];
  let className = '';
  export {className as class};
  export let variant = null;
  export let open = false;

  let element;
  let drawer;
  let listPromiseResolve;
  let listPromise = new Promise(resolve => listPromiseResolve = resolve);

  setContext('SMUI:list:nav', true);
  setContext('SMUI:list:item:nav', true);

  if (variant === 'dismissible' || variant === 'modal') {
    setContext('SMUI:list:instantiate', false);
    setContext('SMUI:list:getInstance', getListInstancePromise);
  }

  $: if (drawer && drawer.open !== open) {
    drawer.open = open;
  }

  onMount(() => {
    if (variant === 'dismissible' || variant === 'modal') {
      drawer = new MDCDrawer(element);
      listPromiseResolve(drawer.list_);
    }
  });

  onDestroy(() => {
    if (drawer) {
      drawer.destroy();
    }
  });

  afterUpdate(() => {
    if (drawer && !(variant === 'dismissible' || variant === 'modal')) {
      drawer.destroy();
      drawer = undefined;
    } else if (!drawer && (variant === 'dismissible' || variant === 'modal')) {
      drawer = new MDCDrawer(element);
      listPromiseResolve(drawer.list_);
    }
  });

  function getListInstancePromise() {
    return listPromise;
  }

  function updateOpen() {
    open = drawer.open;
  }

  export function setOpen(value) {
    open = value;
  }
</script>