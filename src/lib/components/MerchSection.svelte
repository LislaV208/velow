<script lang="ts">
  import { onMount } from 'svelte';
  
  let isVisible = $state(false);
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVisible = true;
        } else {
          isVisible = false;
        }
      });
    }, { threshold: 0.1 });
    
    const section = document.getElementById('merch');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
  
  const merchItems = [
    {
      name: "T-Shirt Tarot",
      price: "70 zł",
      image: "/images/merch/image2115.jpeg",
      description: "Czarny t-shirt z grafiką"
    },
    {
      name: "Bluza z kapturem",
      price: "120 zł",
      image: "/images/merch/image00007.jpeg",
      description: "Czarna bluza z logo zespołu na plecach"
    },
    {
      name: "Album CD 'Wizje'",
      price: "40 zł",
      image: "/images/okladka.png",
      description: "Debiutancki album w digipacku z książeczką"
    },
    {
      name: "T-Shirt 'Logo'",
      price: "70 zł",
      image: "/images/merch/image00001.jpeg",
      description: "Szary t-shirt z nazwą zespołu i logo na plecach"
    },
    {
      name: "Torba płócienna",
      price: "30 zł",
      image: "/images/merch/image00005.jpeg",
      description: "Czarna torba z nadrukiem logo zespołu"
    }
  ];
</script>

<section id="merch" class="section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-800 delay-50 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white">Merch</h2>
      
      <div class="mb-10">
        <p class="text-gray-300 max-w-3xl text-lg">
          Wspieraj zespół kupując nasz oficjalny merch. Wszystkie produkty są wysokiej jakości i zaprojektowane z dbałością o detale.
        </p>
      </div>
      
      <div class="grid sm:grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-8">
        {#each merchItems as item, i}
          <div 
            class=" card rounded-lg overflow-hidden bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
            style="transition-delay: {i * 100}ms"
          >
            <div class="h-70  overflow-hidden relative cursor-pointer flex items-center justify-center">
              <img src={item.image} alt={item.name} class="w-full h-full object-cover transform hover:scale-105 transition-all duration-500">
              <!-- <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div> -->
            </div>
            <div class="p-5 relative">
              <div class="flex justify-between items-start mb-2">
                <h3 class="text-xl font-heading text-white group-hover:text-accent-red transition-colors">{item.name}</h3>
                <span class="bg-gray-800 px-3 py-1 rounded text-white font-medium group-hover:bg-accent-red/20 transition-colors">{item.price}</span>
              </div>
              <p class="text-gray-400 text-sm mb-4">{item.description}</p>
              <a href="/" class="btn w-full text-center border-accent-red text-accent-red hover:text-black">Kontakt</a>
            </div>
          </div>
        {/each}
      </div>
      
      <!-- <div class="mt-12 text-center">
        <p class="text-gray-300 mb-6">Masz pytania dotyczące zamówień lub dostępności produktów?</p>
        <div class="relative inline-block group">
          <a href="#contact" class="btn border-accent-red text-accent-red hover:text-black">Kontakt</a>
          <div class="absolute -inset-0.5 bg-accent-red opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
        </div>
      </div> -->
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>