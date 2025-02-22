<script lang="ts">
  import { twMerge } from 'tailwind-merge';
  import Slide from './Slide.svelte';
  import Thumbnail from './Thumbnail.svelte';
  import Caption from './Caption.svelte';
  import Indicator from './Indicator.svelte';

  export let id: string = 'default-carousel';
  export let showIndicators: boolean = true;
  export let showCaptions: boolean = true;
  export let showThumbs: boolean = true;
  export let images: any[];
  export let slideControls: boolean = true;
  export let loop: boolean = false;
  export let duration: number = 2000;

  // Carousel
  export let divClass: string = 'overflow-hidden relative h-56 rounded-lg sm:h-64 xl:h-80 2xl:h-96';
  let divCls: string = twMerge(divClass, $$props.classDiv);
  export let indicatorDivClass: string = 'flex absolute bottom-5 left-1/2 z-30 space-x-3 -translate-x-1/2';
  let indicatorDivCls: string = twMerge(indicatorDivClass, $$props.classIndicatorDiv);

  // Caption
  export let captionClass: string = 'h-10 bg-gray-300 dark:bg-gray-700 dark:text-white p-2 my-2 text-center';
  let captionCls: string = twMerge(captionClass, $$props.classCaption);

  // Indicator
  export let indicatorClass: string = 'w-3 h-3 rounded-full bg-gray-100 hover:bg-gray-300 opacity-60';
  let indicatorCls: string = twMerge(indicatorClass, $$props.classIndicator);

  // Slide
  export let slideClass: string = 'flex items-center justify-center h-full w-full';
  let slideCls: string = twMerge(slideClass, $$props.classSlide);

  // Img
  export let imgFit: 'cover' | 'contain' | 'fill' | 'none' | 'scale-down' = 'cover';
  export let imgClass: string = `object-${imgFit} ${imgFit === 'cover' && 'w-full'} h-full`;
  let imgCls: string = twMerge(imgClass, $$props.classImg);

  // Thumbnail
  export let thumbClass: string = 'opacity-40';
  let thumbCls: string = twMerge(thumbClass, $$props.classThumb);

  // Thumbnail Container
  export let thumbDivClass: string = 'flex flex-row justify-center bg-gray-100 w-full';
  let thumbDivCls: string = twMerge(thumbDivClass, $$props.classThumbDiv);

  // Thumbnail Img Btn Div
  export let thumbBtnClass: string = '';
  let thumbBtnCls: string = twMerge(thumbBtnClass, $$props.classBtnThumb);

  let imageShowingIndex: number = 0;
  $: image = images[imageShowingIndex];

  const nextSlide = () => {
    if (imageShowingIndex === images.length - 1) {
      imageShowingIndex = 0;
    } else {
      imageShowingIndex += 1;
    }
  };

  const prevSlide = () => {
    if (imageShowingIndex === 0) {
      imageShowingIndex = images.length - 1;
    } else {
      imageShowingIndex -= 1;
    }
  };

  const goToSlide = (number: number) => (imageShowingIndex = number);

  if (loop) {
    setInterval(() => {
      nextSlide();
    }, duration);
  }
</script>

<div {id} class="relative">
  <div class={divCls}>
    <Slide
      image={image.imgurl}
      altTag={image.name}
      attr={image.attribution}
      slideClass={slideCls}
      imgClass={imgCls} />
  </div>
  {#if showIndicators}
    <!-- Slider indicators -->
    <div class={indicatorDivCls}>
      {#each images as { id, imgurl, name, attribution }}
        <Indicator {name} selected={imageShowingIndex === id} on:click={() => goToSlide(id)} indicatorClass={indicatorCls} />
      {/each}
    </div>
  {/if}
  {#if slideControls}
    <!-- Slider controls -->
    <button on:click={prevSlide} type="button" class="flex absolute top-0 left-0 z-30 justify-center items-center px-4 h-full cursor-pointer group focus:outline-none" data-carousel-prev>
      <span class="inline-flex justify-center items-center w-8 h-8 rounded-full sm:w-10 sm:h-10 bg-white/30 dark:bg-gray-800/30 group-hover:bg-white/50 dark:group-hover:bg-gray-800/60 group-focus:ring-4 group-focus:ring-white dark:group-focus:ring-gray-800/70 group-focus:outline-none">
        {#if $$slots.previous}
          <slot name="previous" />
        {:else}
          <svg aria-hidden="true" class="w-5 h-5 text-white sm:w-6 sm:h-6 dark:text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        {/if}
        <span class="hidden">Previous</span>
      </span>
    </button>
    <button on:click={nextSlide} type="button" class="flex absolute top-0 right-0 z-30 justify-center items-center px-4 h-full cursor-pointer group focus:outline-none" data-carousel-next>
      <span class="inline-flex justify-center items-center w-8 h-8 rounded-full sm:w-10 sm:h-10 bg-white/30 dark:bg-gray-800/30 group-hover:bg-white/50 dark:group-hover:bg-gray-800/60 group-focus:ring-4 group-focus:ring-white dark:group-focus:ring-gray-800/70 group-focus:outline-none">
        {#if $$slots.next}
          <slot name="next" />
        {:else}
          <svg aria-hidden="true" class="w-5 h-5 text-white sm:w-6 sm:h-6 dark:text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        {/if}
        <span class="hidden">Next</span>
      </span>
    </button>
  {/if}
</div>

{#if showCaptions}
  <Caption caption={images[imageShowingIndex].name} captionClass={captionCls} />
{/if}

{#if showThumbs}
  <div class={thumbDivCls}>
    {#each images as { id, imgurl, name, attribution }}
      <Thumbnail
        thumbClass={thumbCls}
        thumbBtnClass={thumbBtnCls}
        thumbImg={imgurl}
        altTag={name}
        titleLink={attribution}
        {id}
        selected={imageShowingIndex === id}
        on:click={() => goToSlide(id)} />
    {/each}
  </div>
{/if}

<!--
  @component
  ## Features
  [Go to Carousel](https://flowbite-svelte.com/docs/components/carousel)
  - Setup
  - Default Carousel
  - Loop
  - Without thumbnails
  - Without caption
  - Without indicators
  - Without slide controllers
  - Custom slide controllers
  - Carousel transition
  - Loop
  - Fly example
  - Slide example
  ## Props
  @prop showIndicators: boolean = true;
  @prop showCaptions: boolean = true;
  @prop showThumbs: boolean = true;
  @prop images: any[];
  @prop slideControls: boolean = true;
  @prop loop: boolean = false;
  @prop duration: number = 2000;
  @prop thumbClass: string = 'opacity-40';
  ### Carousel
  @prop divClass: string = 'overflow-hidden relative h-56 rounded-lg sm:h-64 xl:h-80 2xl:h-96';
  @prop indicatorDivClass: string = 'flex absolute bottom-5 left-1/2 z-30 space-x-3 -translate-x-1/2';
  ### Caption
  @prop captionClass: string = 'h-10 bg-gray-300 dark:bg-gray-700 dark:text-white p-2 my-2 text-center';
  ### Indicator
  @prop indicatorClass: string = 'w-3 h-3 rounded-full bg-gray-100 hover:bg-gray-300 opacity-60';
  ### Slide
  @prop slideClass: string = '';
  ## Example
  ```
  <script>
    import { Carousel } from 'flowbite-svelte'
    import { images } from './imageData/+server.js';
  </script>

  <div class="max-w-4xl">
    <Carousel {images} />
  </div>

  ```
-->
