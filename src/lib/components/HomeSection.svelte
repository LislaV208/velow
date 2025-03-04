<script lang="ts">
  import { onMount } from 'svelte';
  
  let isVisible = false;
  
  onMount(() => {
    setTimeout(() => {
      isVisible = true;
    }, 300);
  });
</script>

<section id="home" class="section relative h-screen flex items-center justify-center overflow-hidden">
  <div class="absolute inset-0 bg-black">
    <div class="absolute inset-0 bg-[url('/images/band-bg.jpg')] bg-cover bg-center opacity-50 bg-fixed"></div>
    <div class="absolute inset-0 bg-gradient-to-b from-black/70 via-transparent to-black/70"></div>
  </div>
  
  <div class="container mx-auto px-4 z-10 text-center">
    <div class={`transition-all duration-1000 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <div class="relative inline-block mb-8">
        <img src="/images/velow-logo.png" alt="Velow Logo" class="mx-auto w-64 md:w-96 relative z-10 animate-pulse-slow">
        <div class="absolute -inset-1 bg-gradient-to-r from-accent-red via-transparent to-accent-red opacity-30 blur-lg"></div>
      </div>
      
      <h1 class="text-5xl md:text-7xl font-heading font-bold text-white mb-6 glitch-effect" data-text="VELOW">VELOW</h1>
      
      <p class="text-xl text-gray-300 max-w-2xl mx-auto mb-10 font-light">
        Polski zespół rockowy, który łączy <span class="font-semibold text-white">surową energię</span> z <span class="font-semibold text-white">melodyjnymi kompozycjami</span>
      </p>
      
      <div class="relative inline-block group">
        <a href="#music" class="btn group-hover:bg-accent-red group-hover:border-accent-red">
          <span class="relative z-10">Posłuchaj</span>
        </a>
        <div class="absolute -inset-0.5 bg-accent-red opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-10 left-0 right-0 z-10">
    <nav class="container mx-auto px-4">
      <ul class="flex justify-center space-x-6 md:space-x-10">
        <li><a href="#home" class="nav-link text-white hover:text-accent-silver">Strona Główna</a></li>
        <li><a href="#about" class="nav-link text-white hover:text-accent-silver">O Nas</a></li>
        <li><a href="#music" class="nav-link text-white hover:text-accent-silver">Muzyka</a></li>
        <li><a href="#shows" class="nav-link text-white hover:text-accent-silver">Koncerty</a></li>
        <li><a href="#media" class="nav-link text-white hover:text-accent-silver">Media</a></li>
        <li><a href="#merch" class="nav-link text-white hover:text-accent-silver">Merch</a></li>
        <li><a href="#contact" class="nav-link text-white hover:text-accent-silver">Kontakt</a></li>
      </ul>
    </nav>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>