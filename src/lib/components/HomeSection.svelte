<script lang="ts">
  import { onMount } from 'svelte';
  
  let isVisible = false;
  
  onMount(() => {
    setTimeout(() => {
      isVisible = true;
    }, 300);
  });
</script>


<section class="relative min-h-screen flex flex-col">
  <!-- Tło -->
  <div class="absolute inset-0">
    <div class="absolute inset-0 bg-cover 2xl:bg-[auto_100%] bg-no-repeat bg-center opacity-50" style="background-image: url('/images/home.jpg')"></div>
    <div class="absolute inset-0 bg-gradient-to-b from-black/70 via-transparent to-black/70"></div>
    <div class="absolute inset-0 max-[2048px]:hidden min-[2048px]:w-[2048px] left-1/2 -translate-x-1/2">
      <div class="absolute inset-0 min-[2048px]:bg-gradient-to-l from-transparent from-70% to-black to-100%"></div>
      <div class="absolute inset-0 min-[2048px]:bg-gradient-to-r from-transparent from-70% to-black to-100%"></div>
    </div>
  </div>

  <!-- Kontener treści -->
  <!-- <div class="relative flex-grow flex items-center justify-center"> -->
  <div class="absolute inset-x-0">
    <div class="container mx-auto px-4 text-center z-10">
      <div class="max-w-4xl mx-auto">
        <!-- Tekst i przycisk -->
        <div class="relative max-[1000px]:top-[12vh] max-[2000px]:top-[18vh] top-[40vh]">
          <h1 class="text-6xl md:text-8xl 2xl:text-9xl font-bold text-white mb-4">VELOW</h1>
          <p class="text-lg 2xl:text-4xl text-gray-300 mb-10">
            Polski zespół rockowy, który łączy 
            <span class="font-semibold text-white">surową energię</span> 
            z <span class="font-semibold text-white">melodyjnymi kompozycjami</span>
          </p>
          <button class="px-8 py-3 bg-black text-xl 2xl:text-2xl text-white border border-gray-400 rounded-md  transition-all duration-300 shadow-md hover:shadow-lg transform hover:scale-105">
            Posłuchaj
        </button>
        </div>

      </div>
    </div>

  </div>

  {#snippet navElem(title: string, href: string)}
    <li><a href={href} class="nav-link sm:text-md md:text-md lg:text-xl text-white hover:text-accent-silver">{title}</a></li>
  {/snippet}

  <!-- Nawigacja -->
  <div class="absolute bottom-10 left-0 right-0 z-10">
    <nav class="container mx-auto px-4">
      <ul class="flex justify-center space-x-6 md:space-x-10">
        <!-- {@render navElem('Strona Główna', '#home')} -->
        {@render navElem('O Nas', '#about')}
        {@render navElem('Muzyka', '#music')}
        {@render navElem('Koncerty', '#shows')}
        {@render navElem('Media', '#media')}
        {@render navElem('Merch', '#merch')}
        {@render navElem('Kontakt', '#contact')}

        <!-- <li><a href="#home" class="nav-link text-white hover:text-accent-silver">Strona Główna</a></li> -->
        <!-- <li><a href="#about" class="nav-link text-white hover:text-accent-silver">O Nas</a></li>
        <li><a href="#music" class="nav-link text-white hover:text-accent-silver">Muzyka</a></li>
        <li><a href="#shows" class="nav-link text-white hover:text-accent-silver">Koncerty</a></li>
        <li><a href="#media" class="nav-link text-white hover:text-accent-silver">Media</a></li>
        <li><a href="#merch" class="nav-link text-white hover:text-accent-silver">Merch</a></li>
        <li><a href="#contact" class="nav-link text-white hover:text-accent-silver">Kontakt</a></li> -->
      </ul>
    </nav>
  </div>
</section>

<!-- <section id="home" class="section relative h-screen flex items-center justify-center overflow-hidden">
  <div class="absolute inset-0 bg-black">
    <div class="absolute inset-0 bg-[url('/images/home.jpg')] bg-cover bg-center opacity-50 bg-fixed"></div>
    <div class="absolute inset-0 bg-gradient-to-b from-black/70 via-transparent to-black/70"></div>
  </div>
  
  <div class="container mx-auto px-4 z-10 text-center">
    <div class={`transition-all duration-1000 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      
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
</section> -->