<script>
    import "../app.postcss";
    import {page} from '$app/stores';
    import {Navbar, NavBrand, NavHamburger, NavLi, NavUl, Button, Indicator, Badge} from 'flowbite-svelte';
    import { dev } from '$app/environment';
    import { inject } from '@vercel/analytics';

    inject({ mode: dev ? 'development' : 'production' });
    $: activeUrl = $page.url.pathname;
</script>

<header>
    <Navbar let:NavContainer color="primary">
        <NavContainer class="border px-5 py-2 rounded-lg bg-white">
            <NavBrand href="/">
                <img src="https://flowbite-svelte.com/images/flowbite-svelte-icon-logo.svg" class="mr-3 h-6 sm:h-9"
                     alt="Flowbite Logo"/>
                <span class="self-center whitespace-nowrap text-2xl font-semibold">Super Shoes Info</span>
            </NavBrand>
            <NavHamburger />
            <NavUl class="order-1" {activeUrl}>
                <NavLi href="/" active={true} class="cursor-pointer text-base">
                    <Button class="relative" size="sm">
                        Items
                        <span class="sr-only">Notifications</span>
                    </Button>
                </NavLi>
                <NavLi class="text-base" href="/lowPrice">
                    <Button class="relative" size="sm">
                        Low Price
                        <span class="sr-only">Notifications</span>
                        <Indicator color="blue" border size="xl" placement="top-right" class="text-xs font-bold">N</Indicator>
                    </Button>
                </NavLi>
            </NavUl>
        </NavContainer>
    </Navbar>
</header>


<div class="flex px-4 mx-auto w-full">
    <main class="w-full mx-auto">
        <slot/>
    </main>
</div>