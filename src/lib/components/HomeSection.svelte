<script lang="ts">
  import { onMount } from 'svelte';
  import { ArrowDown } from 'lucide-svelte'
  
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
    <div class="absolute inset-0 bg-cover 2xl:bg-[auto_100%] bg-no-repeat bg-[center_100%] opacity-50" style="background-image: url('/images/home.jpg')"></div>
    <!-- <div class="absolute inset-0 bg-cover 2xl:bg-[auto_100%] bg-no-repeat bg-center opacity-50" style="background-image: url('/images/home.jpg')"></div> -->
    <div class="absolute inset-0 bg-gradient-to-b from-black/70 via-transparent to-black/70"></div>
    <!-- <div class="absolute inset-0 max-[2048px]:hidden min-[2048px]:w-[2048px] left-1/2 -translate-x-1/2">
      <div class="absolute inset-0 min-[2048px]:bg-gradient-to-l from-transparent from-70% to-black to-100%"></div>
      <div class="absolute inset-0 min-[2048px]:bg-gradient-to-r from-transparent from-70% to-black to-100%"></div>
    </div> -->
  </div>

  <!-- Kontener treści -->
  <!-- <div class="relative flex-grow flex items-center justify-center"> -->
  <div class="absolute inset-x-0">
    <div class="container mx-auto px-4 text-center z-10">
      <div class="max-w-lg 2xl:max-w-6xl mx-auto">
        <!-- Tekst i przycisk -->
        <div class="relative max-[1000px]:top-[12vh] max-[2000px]:top-[16vh] top-[24vh]">
          <h1 class="text-6xl md:text-8xl 2xl:text-[256px] font-bold text-white mb-4">VELOW</h1>
          <p class="text-lg 2xl:text-5xl text-gray-300 mb-10">
            Polski zespół rockowy, który łączy 
            <span class="font-semibold text-white">surową energię</span> 
            z <span class="font-semibold text-white">melodyjnymi kompozycjami</span>
          </p>
          <button class="px-8 py-3 bg-black text-xl 2xl:text-5xl text-white border border-gray-400 rounded-md  transition-all duration-300 shadow-md hover:shadow-lg transform hover:scale-105">
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
  <!-- <div class="max-sm:hidden absolute py-8 bottom-0 left-0 right-0 z-10 bg-black/50"> -->
  <div class="max-sm:hidden absolute py-8 bottom-0 left-0 right-0 z-10 bg-linear-to-t from-black to-transparent">
    <nav class="container mx-auto px-4">
      <ul class="flex justify-center space-x-6 md:space-x-10">
        {@render navElem('O Nas', '#about')}
        {@render navElem('Muzyka', '#music')}
        {@render navElem('Koncerty', '#shows')}
        {@render navElem('Media', '#media')}
        {@render navElem('Merch', '#merch')}
        {@render navElem('Kontakt', '#contact')}
      </ul>
    </nav>
  </div>
  <button class="sm:hidden border border-gray-500 absolute bottom-5 rounded-full left-1/2 -translate-x-1/2 text-white text-4xl animate-[bounce_2s_ease-in-out_infinite] bg-black size-12">
    <ArrowDown class="m-auto" />
  </button>
</section>