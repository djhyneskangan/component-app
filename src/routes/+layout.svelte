
<script>
	import '../app.postcss';
    import { Navbar, NavBrand, NavLi, NavUl, NavHamburger, Button, Input } from 'flowbite-svelte'
	import { Footer, FooterCopyright, FooterLinkGroup, FooterLink } from 'flowbite-svelte'
	//import JournalEntries from './journalEntries.svelte';
	//import NewEntry from './newEntry.svelte';

</script>

  <Navbar let:hidden let:toggle>
	<NavBrand href="/">
	  <img
		src="https://img.logoipsum.com/258.svg"
		class="mr-3 h-6 sm:h-9"
		alt="Flowbite Logo"
	  />
	</NavBrand>



	<div class="flex md:order-2">
	  <Button color="none" data-collapse-toggle="mobile-menu-3" aria-controls="mobile-menu-3" aria-expanded="false" class="md:hidden text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 rounded-lg text-sm p-2.5 mr-1" >
		<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 dark:text-white"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" /></svg>
	  </Button>
	  <div class="hidden relative md:block">
		<div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
		  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 dark:text-white"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" /></svg>
		</div>
		<Input id="search-navbar" class="pl-10" placeholder="Search..." />
	  </div>

	  <!-- <div class="pl-6">
	  <NewEntry />
		</div> -->

	  <NavHamburger on:click={toggle} />
	</div>
	<NavUl {hidden}>
	  <NavLi href="/" active={true}>Home</NavLi>
	  <NavLi href="/about">About</NavLi>
	  <NavLi href="/services">Services</NavLi>
	  <NavLi href="/entries">Entries</NavLi>
	</NavUl>
  </Navbar>


<slot />

<Footer>
	<FooterCopyright href="/" by="Flowbite™" year={2023} />
	<FooterLinkGroup ulClass="flex flex-wrap items-center mt-3 text-sm text-gray-500 dark:text-gray-400 sm:mt-0">
	  <FooterLink href="/">About</FooterLink>
	  <FooterLink href="/">Privacy Policy</FooterLink>
	  <FooterLink href="/">Licensing</FooterLink>
	  <FooterLink href="/">Contact</FooterLink>
	</FooterLinkGroup>
  </Footer>

  <style>
	:global(body) {
		padding: 0px 20px;
	}
  </style>