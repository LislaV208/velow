<script lang="ts">
  import { onMount } from 'svelte';
  
  let scrollY: number;
  let isScrolled = $state(false);
  let isVisible = $state(false);
  let isMobileMenuOpen = $state(false);
  let menuRef: HTMLElement;
  let buttonRef: HTMLElement;
  
  onMount(() => {
    const handleScroll = () => {
      scrollY = window.scrollY;
      // console.log('scrollY: ' + scrollY + 'px');
      // isScrolled = scrollY > 777;
      isScrolled = true;
      isVisible = scrollY > window.innerHeight * 0.88; 
    };
    
    const handleClickOutside = (event: MouseEvent) => {
      if (isMobileMenuOpen && menuRef && buttonRef) {
        const target = event.target as Node;
        if (!menuRef.contains(target) && !buttonRef.contains(target)) {
          closeMobileMenu();
        }
      }
    };
    
    window.addEventListener('scroll', handleScroll);
    document.addEventListener('click', handleClickOutside);
    
    return () => {
      window.removeEventListener('scroll', handleScroll);
      document.removeEventListener('click', handleClickOutside);
    };
  });
  
  function toggleMobileMenu(): void {
    isMobileMenuOpen = !isMobileMenuOpen;
  }
  
  function closeMobileMenu(): void {
    isMobileMenuOpen = false;
  }
</script>

<header class={`fixed top-0 left-0 w-full z-50 transition-all duration-200 ${isScrolled ? 'bg-black border-2 border-black border-b-white/20 py-5' : 'bg-transparent'} ${isVisible ? 'translate-y-0' : '-translate-y-full'}`}>
  <div class="container mx-auto px-4 flex justify-between items-center">
    <a href="#home" class="text-white text-3xl font-bold relative tracking-wider overflow-visible group">
      <h1 class="relative z-10 inline-block transition-transform duration-300 group-hover:scale-110" style="font-family: 'BluPurpl', sans-serif !important; text-transform: none;">veLOw</h1>
      <span class="absolute bottom-0 left-0 w-full h-0.5 bg-accent-silver transform scale-x-0 transition-transform duration-300 group-hover:scale-x-100"></span>
    </a>
    
    <nav class="hidden md:block">
      <ul class="flex space-x-8 ">
        <li><a href="#about" class="nav-link text-white hover:text-accent-silver text-2xl">O Nas</a></li>
        <li><a href="#music" class="nav-link text-white hover:text-accent-silver text-2xl">Muzyka</a></li>
        <li><a href="#shows" class="nav-link text-white hover:text-accent-silver text-2xl">Koncerty</a></li>
        <!-- <li><a href="#media" class="nav-link text-white hover:text-accent-silver">Media</a></li> -->
        <li><a href="#merch" class="nav-link text-white hover:text-accent-silver text-2xl">Merch</a></li>
        <li><a href="#contact" class="nav-link text-white hover:text-accent-silver text-2xl">Kontakt</a></li>
      </ul>
    </nav>
    
    <button 
      class="md:hidden text-white relative z-10 w-10 h-10 flex items-center justify-center" 
      aria-label="Menu"
      onclick={() => toggleMobileMenu()}
      bind:this={buttonRef}
    >
      <div class="w-6 flex flex-col items-center justify-center">
        <span class="block w-full h-0.5 bg-white mb-1.5 transition-all duration-300 transform {isMobileMenuOpen ? 'rotate-45 translate-y-2' : ''}"></span>
        <span class="block w-full h-0.5 bg-white mb-1.5 transition-all duration-300 {isMobileMenuOpen ? 'opacity-0' : 'opacity-100'}"></span>
        <span class="block {isMobileMenuOpen ? 'w-full' : 'w-3/4'} h-0.5 bg-white transition-all duration-300 transform {isMobileMenuOpen ? '-rotate-45 -translate-y-2' : ''} {isMobileMenuOpen ? '' : 'self-end'}"></span>
      </div>
    </button>
  </div>
</header>

<!-- Mobilne menu -->
<div 
  class="md:hidden fixed top-10 left-0 w-full bg-black border-b-2 border-white/20 z-40 transition-all duration-300 overflow-hidden"
  style="max-height: {isMobileMenuOpen ? '400px' : '0'}; opacity: {isMobileMenuOpen ? '1' : '0'}; transform: translateY({isMobileMenuOpen ? '0' : '-10px'});"
  bind:this={menuRef}
>
  <nav class="w-full px-6 py-4">
    <ul class="flex flex-col space-y-4 text-center">
      <li><a href="#about" class="nav-link text-white text-xl hover:text-accent-silver block py-1" onclick={() => closeMobileMenu()}>O Nas</a></li>
      <li><a href="#music" class="nav-link text-white text-xl hover:text-accent-silver block py-1" onclick={() => closeMobileMenu()}>Muzyka</a></li>
      <li><a href="#shows" class="nav-link text-white text-xl hover:text-accent-silver block py-1" onclick={() => closeMobileMenu()}>Koncerty</a></li>
      <li><a href="#merch" class="nav-link text-white text-xl hover:text-accent-silver block py-1" onclick={() => closeMobileMenu()}>Merch</a></li>
      <li><a href="#contact" class="nav-link text-white text-xl hover:text-accent-silver block py-1" onclick={() => closeMobileMenu()}>Kontakt</a></li>
    </ul>
  </nav>
</div>