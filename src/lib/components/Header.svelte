<script lang="ts">
  import { onMount } from 'svelte';
  
  let scrollY: number;
  let isScrolled = $state(false);
  let isVisible = $state(false);
  
  onMount(() => {
    const handleScroll = () => {
      scrollY = window.scrollY;
      // console.log('scrollY: ' + scrollY + 'px');
      // isScrolled = scrollY > 777;
      isScrolled = true;
      isVisible = scrollY > window.innerHeight * 0.88; 
    };
    
    window.addEventListener('scroll', handleScroll);
    
    return () => {
      window.removeEventListener('scroll', handleScroll);
    };
  });
</script>

<header class={`fixed top-0 left-0 w-full z-50 transition-all duration-200 ${isScrolled ? 'bg-black border-2 border-black border-b-white/20 py-5' : 'bg-transparent'} ${isVisible ? 'translate-y-0' : '-translate-y-full'}`}>
  <div class="container mx-auto px-4 flex justify-between items-center">
    <a href="#home" class="text-white text-3xl font-bold relative tracking-wider overflow-hidden group">
      <h1 class="relative z-10 inline-block transition-transform duration-300 group-hover:scale-110">VELOW</h1>
      <span class="absolute bottom-0 left-0 w-full h-0.5 bg-accent-silver transform scale-x-0 transition-transform duration-300 group-hover:scale-x-100"></span>
    </a>
    
    <nav class="hidden md:block">
      <ul class="flex space-x-8">
        <li><a href="#home" class="nav-link text-white hover:text-accent-silver">Start</a></li>
        <li><a href="#about" class="nav-link text-white hover:text-accent-silver">O Nas</a></li>
        <li><a href="#music" class="nav-link text-white hover:text-accent-silver">Muzyka</a></li>
        <li><a href="#shows" class="nav-link text-white hover:text-accent-silver">Koncerty</a></li>
        <li><a href="#media" class="nav-link text-white hover:text-accent-silver">Media</a></li>
        <li><a href="#merch" class="nav-link text-white hover:text-accent-silver">Merch</a></li>
        <li><a href="#contact" class="nav-link text-white hover:text-accent-silver">Kontakt</a></li>
      </ul>
    </nav>
    
    <button class="md:hidden text-white relative z-10 w-10 h-10 flex items-center justify-center" aria-label="Menu">
      <div class="w-6 flex flex-col items-center justify-center">
        <span class="block w-full h-0.5 bg-white mb-1.5 transition-all duration-300"></span>
        <span class="block w-full h-0.5 bg-white mb-1.5 transition-all duration-300"></span>
        <span class="block w-3/4 h-0.5 bg-white transition-all duration-300 self-end"></span>
      </div>
    </button>
  </div>
</header>