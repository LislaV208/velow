<script lang="ts">
  import { onMount } from 'svelte';
  
  let isVisible = false;
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVisible = true;
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
      name: "T-Shirt 'Pierwszy Krok'",
      price: "89 zł",
      image: "/images/merch-tshirt1.jpg",
      description: "Czarny t-shirt z grafiką z okładki albumu"
    },
    {
      name: "Bluza z kapturem",
      price: "159 zł",
      image: "/images/merch-hoodie.jpg",
      description: "Czarna bluza z logo zespołu na plecach"
    },
    {
      name: "Album CD 'Pierwszy Krok'",
      price: "49 zł",
      image: "/images/merch-cd.jpg",
      description: "Debiutancki album w digipacku z książeczką"
    },
    {
      name: "Winyl 'Pierwszy Krok'",
      price: "119 zł",
      image: "/images/merch-vinyl.jpg",
      description: "Limitowana edycja na czarnym winylu"
    },
    {
      name: "T-Shirt 'Logo'",
      price: "79 zł",
      image: "/images/merch-tshirt2.jpg",
      description: "Szary t-shirt z minimalistycznym logo zespołu"
    },
    {
      name: "Torba płócienna",
      price: "49 zł",
      image: "/images/merch-bag.jpg",
      description: "Czarna torba z nadrukiem logo zespołu"
    }
  ];
</script>

<section id="merch" class="section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-1000 delay-300 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white">Merch</h2>
      
      <div class="mb-10">
        <p class="text-gray-300 max-w-3xl text-lg">
          Wspieraj zespół kupując nasz oficjalny merch. Wszystkie produkty są wysokiej jakości i zaprojektowane z dbałością o detale.
        </p>
      </div>
      
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
        {#each merchItems as item, i}
          <div 
            class="card rounded-lg overflow-hidden bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
            style="transition-delay: {i * 100}ms"
          >
            <div class="aspect-square overflow-hidden relative">
              <img src={item.image} alt={item.name} class="w-full h-full object-cover transform hover:scale-105 transition-all duration-500">
              <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
            </div>
            <div class="p-5 relative">
              <div class="flex justify-between items-start mb-2">
                <h3 class="text-xl font-heading text-white group-hover:text-accent-red transition-colors">{item.name}</h3>
                <span class="bg-gray-800 px-3 py-1 rounded text-white font-medium group-hover:bg-accent-red/20 transition-colors">{item.price}</span>
              </div>
              <p class="text-gray-400 text-sm mb-4">{item.description}</p>
              <a href="#" class="btn w-full text-center border-accent-red text-accent-red hover:text-black">Kup teraz</a>
            </div>
          </div>
        {/each}
      </div>
      
      <div class="mt-12 text-center">
        <p class="text-gray-300 mb-6">Masz pytania dotyczące zamówień lub dostępności produktów?</p>
        <div class="relative inline-block group">
          <a href="mailto:merch@velow.pl" class="btn border-accent-red text-accent-red hover:text-black">Kontakt - Merch</a>
          <div class="absolute -inset-0.5 bg-accent-red opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
        </div>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>