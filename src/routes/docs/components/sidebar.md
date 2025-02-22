---
layout: componentLayout
title: Svelte Sidebar - Flowbite
breadcrumb_title: Svelte Sidebar
component_title: Sidebar
dir: Components
description: Use the sidebar component to show a list of menu items and multi-level dropdown items on either side of the page to navigate on your website
thumnailSize: w-72
---

<script>
  import { page } from '$app/stores';
  import { TableProp, TableDefaultRow, DocBadgeList } from '../../utils'
  import { Badge, Heading, P, A } from '$lib'
  import { props as items } from '../../props/Sidebar.json'
  import { props as items2 }  from '../../props/SidebarBrand.json'
  import { props as items3 }  from '../../props/SidebarCta.json'
  import { props as items4 }  from '../../props/SidebarDropdownItem.json'
  import { props as items5 }  from '../../props/SidebarDropdownWrapper.json'
  import { props as items6 }  from '../../props/SidebarGroup.json'
  import { props as items7 }  from '../../props/SidebarItem.json'
  import { props as items8 }  from '../../props/SidebarWrapper.json'

  const events = ["on:blur","on:click","on:focus","on:keydown","on:keypress","on:keyup","on:mouseenter","on:mouseleave","on:mouseover"];
</script>

The sidebar component can be used as a complementary element relative to the navbar shown on either the left or right side of the page used for the navigation on your web application, including menu items, multi-level dropdown items, call to actions elements, and more.

Disclaimer: this sidebar component is based on this <A class="text-primary-700" href="https://github.com/shinokada/svelte-sidebar" target="_blank" rel="noreferrer">sidebar menu</A> plugin.

## Setup

```svelte example hideOutput
<script>
  import { Sidebar, SidebarBrand, SidebarCta, SidebarDropdownItem, SidebarDropdownWrapper, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
</script>
```

## Default sidebar

Use this example to show a responsive list of menu items inside the sidebar with icons and labels.

```svelte example
<script>
  import { page } from '$app/stores';
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
  import { Icon } from 'flowbite-svelte-icons';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
  $: activeUrl = $page.url.pathname;
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard">
        <svelte:fragment slot="icon">
          <Icon name="chart-pie-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Kanban" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="grid-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center px-2 ml-3 text-sm font-medium text-gray-800 bg-gray-200 rounded-full dark:bg-gray-700 dark:text-gray-300"> Pro </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Inbox" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="mail-box-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center p-3 ml-3 w-3 h-3 text-sm font-medium text-primary-600 bg-primary-200 rounded-full dark:bg-primary-900 dark:text-primary-200"> 3 </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sidebar" href="/docs/components/sidebar" active={activeUrl === '/docs/components/sidebar'}>
        <svelte:fragment slot="icon">
          <Icon name="user-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign In">
        <svelte:fragment slot="icon">
          <Icon name="arrow-right-to-bracket-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign Up">
        <svelte:fragment slot="icon">
          <Icon name="file-edit-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

## Multi-level dropdown

Use this sidebar example to create multi-level menu items by using the dSidebarDropdownWrapper and SidebarDropdownItem components.

```svelte example
<script>
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarDropdownItem, SidebarDropdownWrapper } from 'flowbite-svelte';
  import { Icon } from 'flowbite-svelte-icons';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard">
        <svelte:fragment slot="icon">
          <Icon name="chart-pie-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarDropdownWrapper label="E-commerce">
        <svelte:fragment slot="icon">
          <Icon name="shopping-cart-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <SidebarDropdownItem label="Products" />
        <SidebarDropdownItem label="Billing" />
        <SidebarDropdownItem label="Invoice" />
      </SidebarDropdownWrapper>
      <SidebarItem label="Kanban" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="grid-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center px-2 ml-3 text-sm font-medium text-gray-800 bg-gray-200 rounded-full dark:bg-gray-700 dark:text-gray-300"> Pro </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Inbox" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="mail-box-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center p-3 ml-3 w-3 h-3 text-sm font-medium text-primary-600 bg-primary-200 rounded-full dark:bg-primary-900 dark:text-primary-200"> 3 </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Users">
        <svelte:fragment slot="icon">
          <Icon name="user-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign In">
        <svelte:fragment slot="icon">
          <Icon name="arrow-right-to-bracket-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign Up">
        <svelte:fragment slot="icon">
          <Icon name="file-edit-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

You can change the icons using `arrowup` and `arrowdown` slots.

```svelte example
<script>
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarDropdownItem, SidebarDropdownWrapper } from 'flowbite-svelte';
  import { Icon } from 'flowbite-svelte-icons';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard">
        <svelte:fragment slot="icon">
          <Icon name="chart-pie-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarDropdownWrapper label="E-commerce">
        <svelte:fragment slot="icon">
          <Icon name="shopping-cart-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="arrowup">
          <Icon name="chevron-double-up-outline" class="w-3 h-3" />
        </svelte:fragment>
        <svelte:fragment slot="arrowdown">
          <Icon name="chevron-double-down-outline" class="w-3 h-3" />
        </svelte:fragment>
        <SidebarDropdownItem label="Products" />
        <SidebarDropdownItem label="Billing" />
        <SidebarDropdownItem label="Invoice" />
      </SidebarDropdownWrapper>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

## Active item

Use the following example to show the active item. Use the `activeClass` prop to change the style.

```svelte example
<script>
  import { page } from '$app/stores';
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
  $: activeUrl = $page.url.pathname;
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard" href="/dashboard" active={activeUrl === '/dashboard'} />
      <SidebarItem label="Sidebar" href="/docs/component/sidebar" active={activeUrl === '/docs/components/sidebar'} />
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

```svelte example
<script>
  import { page } from '$app/stores';
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarDropdownWrapper, SidebarDropdownItem } from 'flowbite-svelte';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
  $: activeUrl = $page.url.pathname;
  $: containPath = () => {
    // add your logic here
    true;
  };
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard" active={activeUrl === '/dashboard'} />
      <SidebarDropdownWrapper label="E-commerce" isOpen={containPath}>
        <SidebarDropdownItem label="Products" href="/components/products" active={activeUrl === '/components/products'} />
        <SidebarDropdownItem label="Sidebar" href="/docs/components/sidebar" active={activeUrl === '/docs/components/sidebar'} />
      </SidebarDropdownWrapper>
      <SidebarDropdownWrapper label="Items">
        <SidebarDropdownItem label="Item 1" href="/components/item1" active={activeUrl === '/components/item'} />
        <SidebarDropdownItem label="Item 2" href="/components/item2" active={activeUrl === '/components/billing'} />
      </SidebarDropdownWrapper>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

## Content separator

Separate the content inside the sidebar component by applying a border separator to the SidebarGroup component.

```svelte example
<script>
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
  import { Icon } from 'flowbite-svelte-icons';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard">
        <svelte:fragment slot="icon">
          <Icon name="chart-pie-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Kanban" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="grid-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center px-2 ml-3 text-sm font-medium text-gray-800 bg-gray-200 rounded-full dark:bg-gray-700 dark:text-gray-300"> Pro </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Inbox" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="mail-box-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center p-3 ml-3 w-3 h-3 text-sm font-medium text-primary-600 bg-primary-200 rounded-full dark:bg-primary-900 dark:text-primary-200"> 3 </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Users">
        <svelte:fragment slot="icon">
          <Icon name="user-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Products">
        <svelte:fragment slot="icon">
          <Icon name="bag-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign In">
        <svelte:fragment slot="icon">
          <Icon name="arrow-right-to-bracket-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign Up">
        <svelte:fragment slot="icon">
          <Icon name="file-edit-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
    </SidebarGroup>
    <SidebarGroup border>
      <SidebarItem label="Upgrade to Pro">
        <svelte:fragment slot="icon">
          <Icon name="fire-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Documentation">
        <svelte:fragment slot="icon">
          <Icon name="book-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Components">
        <svelte:fragment slot="icon">
          <Icon name="window-restore-outline" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Help">
        <svelte:fragment slot="icon">
          <Icon name="life-buoy-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

## CTA button

Use this example to add a CTA button inside the sidebar component and encourage your users to visit the dedicated page.

```svelte example
<script>
  import { page } from '$app/stores';
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarCta } from 'flowbite-svelte';
  import { Icon } from 'flowbite-svelte-icons';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard">
        <svelte:fragment slot="icon">
          <Icon name="chart-pie-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Kanban" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="grid-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center px-2 ml-3 text-sm font-medium text-gray-800 bg-gray-200 rounded-full dark:bg-gray-700 dark:text-gray-300"> Pro </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Inbox" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="mail-box-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center p-3 ml-3 w-3 h-3 text-sm font-medium text-primary-600 bg-primary-200 rounded-full dark:bg-primary-900 dark:text-primary-200"> 3 </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Users">
        <svelte:fragment slot="icon">
          <Icon name="user-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign In">
        <svelte:fragment slot="icon">
          <Icon name="arrow-right-to-bracket-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign Up">
        <svelte:fragment slot="icon">
          <Icon name="file-edit-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarCta label="Beta">
        <svelte:fragment slot="icon">
          <button type="button" class="ml-auto -mx-1.5 -my-1.5 bg-primary-50 text-primary-900 rounded-lg focus:ring-2 focus:ring-primary-400 p-1 hover:bg-primary-200 inline-flex h-6 w-6 dark:bg-primary-900 dark:text-primary-400 dark:hover:bg-primary-800" data-collapse-toggle="dropdown-cta" aria-label="Close">
            <span class="sr-only">Close</span>
            <Icon name="close-outline" class="w-2 h-2" />
          </button>
        </svelte:fragment>
        <p class="mb-3 text-sm text-primary-900 dark:text-primary-400">Preview the new Flowbite dashboard navigation! You can turn the new navigation off for a limited time in your profile.</p>
        <a class="text-sm text-primary-900 underline hover:text-primary-800 dark:text-primary-400 dark:hover:text-primary-300" href="/"> Turn new navigation off </a>
      </SidebarCta>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

## Logo branding

Show the logo of your brand and link back to the homepage from the top part of the sidebar.

```svelte example
<script>
  import { Sidebar, SidebarWrapper, SidebarBrand, SidebarItem, SidebarGroup } from 'flowbite-svelte';
  import { Icon } from 'flowbite-svelte-icons';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';

  let site = {
    name: 'Flowbite-Svelte',
    href: '/',
    img: '/images/flowbite-svelte-icon-logo.svg'
  };
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarBrand {site} />
      <SidebarItem label="Dashboard">
        <svelte:fragment slot="icon">
          <Icon name="chart-pie-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Kanban" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="grid-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center px-2 ml-3 text-sm font-medium text-gray-800 bg-gray-200 rounded-full dark:bg-gray-700 dark:text-gray-300"> Pro </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Inbox" {spanClass}>
        <svelte:fragment slot="icon">
          <Icon name="mail-box-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
        <svelte:fragment slot="subtext">
          <span class="inline-flex justify-center items-center p-3 ml-3 w-3 h-3 text-sm font-medium text-primary-600 bg-primary-200 rounded-full dark:bg-primary-900 dark:text-primary-200"> 3 </span>
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Users">
        <svelte:fragment slot="icon">
          <Icon name="user-solid" class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign In">
        <svelte:fragment slot="icon">
          <Icon name="arrow-right-to-bracket-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
      <SidebarItem label="Sign Up">
        <svelte:fragment slot="icon">
          <Icon name="file-edit-solid"  class="w-5 h-5 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
        </svelte:fragment>
      </SidebarItem>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

## Transition

You can add own transition by setting `transitionType` and `transitionParams`.

```svelte example
<script>
  import { page } from '$app/stores';
  import { sineIn } from 'svelte/easing';
  import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarDropdownWrapper, SidebarDropdownItem } from 'flowbite-svelte';
  let spanClass = 'flex-1 ml-3 whitespace-nowrap';
  $: activeUrl = $page.url.pathname;
  $: containPath = () => {
    // add your logic here
    true;
  };
  let transitionParams = {
    x: -320,
    duration: 200,
    easing: sineIn
  };
</script>

<Sidebar>
  <SidebarWrapper>
    <SidebarGroup>
      <SidebarItem label="Dashboard" active={activeUrl === '/dashboard'} />
      <SidebarDropdownWrapper label="E-commerce" isOpen={containPath} transitionType="fly" {transitionParams}>
        <SidebarDropdownItem label="Products" href="/components/products" active={activeUrl === '/components/products'} />
        <SidebarDropdownItem label="Sidebar" href="/docs/components/sidebar" active={activeUrl === '/docs/components/sidebar'} />
      </SidebarDropdownWrapper>
      <SidebarDropdownWrapper label="Items" transitionType="fly" {transitionParams}>
        <SidebarDropdownItem label="Item 1" href="/components/item1" active={activeUrl === '/components/item'} />
        <SidebarDropdownItem label="Item 2" href="/components/item2" active={activeUrl === '/components/billing'} />
      </SidebarDropdownWrapper>
    </SidebarGroup>
  </SidebarWrapper>
</Sidebar>
```

## Props

The component has the following props, type, and default values. See [types page](/docs/pages/typescript) for type information.

### Sidebar

- Use the `class` prop to overwrite `asideClass`.

<TableProp>
  <TableDefaultRow {items} rowState='hover' />
</TableProp>

### SidebarBrand

- Use the `class` prop to overwrite `aClass`.

<TableProp>
  <TableDefaultRow items={items2} rowState='hover' />
</TableProp>

### SidebarCta

- Use the `class` prop to overwrite the default class.

<TableProp>
  <TableDefaultRow items={items3} rowState='hover' />
</TableProp>

### SidebarDropdownItem

- Use the `class` prop to overwrite `divWrapperClass`.

<TableProp>
  <TableDefaultRow items={items4} rowState='hover' />
</TableProp>

### SidebarDropdownWrapper

- Use the `class` prop to overwrite `btnClass`.

<TableProp>
  <TableDefaultRow items={items5} rowState='hover' />
</TableProp>

### SidebarGroup

- Use the `class` prop to overwrite `ulClass`.

<TableProp>
  <TableDefaultRow items={items6} rowState='hover' />
</TableProp>

### SidebarItem

- Use the `class` prop to overwrite the `a` tag class.

<TableProp>
  <TableDefaultRow items={items7} rowState='hover' />
</TableProp>

### SidebarWrapper

- Use the `class` prop to overwrite `divClass`.

<TableProp>
  <TableDefaultRow items={items8} rowState='hover' />
</TableProp>

## Forwarded Events

### SidebarDropdownItem, SidebarItem

<DocBadgeList items={events} />

## References

- [Flowbite Sidebar](https://flowbite.com/docs/components/sidebar/)
