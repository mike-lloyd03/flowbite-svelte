<script lang="ts">
  import { twMerge } from 'tailwind-merge';
  export let svgClass: string = 'w-4 h-4';
</script>

<svg {...$$restProps} class={twMerge(svgClass, $$props.class)} aria-hidden="true" fill="currentColor" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512">
  <path d="M118.6 105.4l128 127.1C252.9 239.6 256 247.8 256 255.1s-3.125 16.38-9.375 22.63l-128 127.1c-9.156 9.156-22.91 11.9-34.88 6.943S64 396.9 64 383.1V128c0-12.94 7.781-24.62 19.75-29.58S109.5 96.23 118.6 105.4z" />
</svg>

<!--
  @component
  ## Features
  [Go to KBD](https://flowbite-svelte.com/docs/components/kbd)
  ## Props
  @prop svgClass: string = 'w-4 h-4';
-->
