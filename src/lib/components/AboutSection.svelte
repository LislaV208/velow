<script lang="ts">
  import { onMount } from 'svelte';
  import emblaCarouselSvelte from 'embla-carousel-svelte'
  import Autoplay from 'embla-carousel-autoplay'
  
  let isVisible = $state(false);

  let options = {};
  let plugins = [Autoplay({stopOnInteraction:false, delay: 8000, stopOnFocusIn: true})]
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVisible = true;
          console.log('visible');
        } else {
          isVisible = false;
          console.log('hidden');
        }
      });
    }, { threshold: 0.1 });
    
    const section = document.getElementById('about');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
  
  const bandMembers = [
    {
      name: "Eryk",
      role: "Wokal",
      image: "/images/eryk.JPG",
      bio: "Czasem coś murknie do mikrofonu, czasem ryknie - a czasem spawa kurczaki"
    },
    {
      name: "Tomek",
      role: "Gitara",
      image: "/images/tomek.jpg",
      bio: "Koleś git(arzysta), zespołowy ogarniacz i polski Mr. Beast"
    },
    {
      name: "Lisu",
      role: "Gitara",
      image: "/images/lisu.jpg",
      bio: "Jeżeli wybierasz się na jakikolwiek koncert to masz 50% szans na to, że pojawi się na scenie"
    },
    {
      name: "Wiktor",
      role: "Bas",
      image: "/images/wiktor.jpg",
      bio: "Fanki do niego lgną, ale koszulki niekoniecznie. Sigma Skidibi Nike Pro"
    },
    {
      name: "Krystian",
      role: "Perkusja",
      image: "/images/krystian.jpg",
      bio: "Jego ulubiony utwór to: Metronome - 120bpm"
    }
  ];
</script>

<section id="about" class="max-sm:px-1! section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-800 delay-50 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="text-5xl! section-title text-white">O Nas</h2>
      
      <!-- <div class="grid grid-cols-1 md:grid-cols-2 gap-10 mb-16"> -->
      <div class="flex max-sm:flex-col flex-row gap-10 mb-16">
        <div class="flex-2">
          <p class="text-gray-300 mb-6 max-sm:text-md md:text-lg">
            Velow to powstały w roku 2021 zespół, muzycznie będący w klimatach rocka alternatywnego. Po pierwszych, bardzo intensywnych dwóch latach działalności, miało miejsce nasze pierwsze wyjście z mroku z naszym debiutanckim albumem pod tytułem “Wizje”, który przyjął się bardzo dobrze w środowisku. Razem z premierą, w 2023 wyruszyliśmy w trasę “Wizje Tour”, odwiedzając takie miasta jak Szczecin, Gdańsk, Poznań. Nasza muzyka to pewna opowieść. To enigmatyczne teksty, które w połączeniu z energiczną muzyką tworzą mieszankę wybuchową. 
          </p>
          <p class="text-gray-300 mb-6 max-sm:text-md md:text-lg">
            Mamy za sobą dwukrotny występ na Szczecińskich Juwenaliach, w naszej dotychczasowej karierze graliśmy między innymi przed takimi zespołami jak: Lady Pank, Kult, Enej, Organek
          </p>
          <p class="text-gray-300 sm:text-md md:text-lg">
            "Jeśli takie są "Wizje" przyszłości polskiego rocka, to jest dobrze, naprawdę dobrze!" - EskaROCK "Velow bywają i czadowi (przewrotna Smutna Piosenka), i refleksyjni (Mimo Strat, Miasto pełne krzyku). I w każdym wcieleniu im do twarzy" - TerazROCK
          </p>
          
          <div class="mt-8 flex justify-center w-full">
            <a href="#music" class="btn hover:text-black">
              Posłuchaj naszej muzyki
            </a>
          </div>
        </div>
        <div class="flex-1 embla " use:emblaCarouselSvelte="{{options, plugins}}">
            <div class="embla__container">
              {#each bandMembers as member, i}
              <div class="{i < bandMembers.length - 1 ? 'mr-5' : 'mr-0'} embla__slide card p-5 rounded-lg bg-black/50 backdrop-blur-sm">
                <div class="relative mb-4 overflow-hidden rounded-lg aspect-square">
                  <!-- <img src={member.image} alt={member.name} class="w-full h-full object-cover grayscale"> -->
                  <img src={member.image} alt={member.name} class="w-full h-full object-cover grayscale"
                  style="object-position: center {member.name === 'Eryk' ? '70%' : member.name === 'Lisu' ? '0%': member.name === 'Wiktor' ? '30%' : member.name === 'Krystian' ? '30%' : '50%'}"
                  >
                  <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div>
                  <div class="absolute bottom-0 left-0 w-full p-3">
                    <h4 class="text-xl text-white">{member.name}</h4>
                    <p class="text-sm">{member.role}</p>
                  </div>
                </div>
                <p class="text-gray-400 text-sm">{member.bio}</p>
              </div>
            {/each}
            </div>
          <!-- </div> -->
          <!-- <div class="absolute -inset-4 bg-gradient-to-r from-accent-red to-transparent opacity-10 blur-lg"></div>
          <img src="/images/band-about.jpg" alt="Zespół Velow" class="w-full h-auto rounded-lg shadow-2xl relative z-10 grayscale hover:grayscale-0 transition-all duration-700">
          <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent rounded-lg"></div> -->
          <!-- <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            {#each bandMembers as member, i}
              <div class="card p-5 rounded-lg bg-black/50 backdrop-blur-sm" style="transition-delay: {i * 100}ms">
                <div class="relative mb-4 overflow-hidden rounded-lg aspect-square">
                  <img src={member.image} alt={member.name} class="w-full h-full object-cover grayscale hover:grayscale-0 transition-all duration-500">
                  <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div>
                  <div class="absolute bottom-0 left-0 w-full p-3">
                    <h4 class="text-xl font-heading text-white mb-0">{member.name}</h4>
                    <p class="text-accent-red text-sm">{member.role}</p>
                  </div>
                </div>
                <p class="text-gray-400 text-sm">{member.bio}</p>
              </div>
            {/each}
          </div> -->
          
        </div>
      </div>


      
      <!-- <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        {#each bandMembers as member, i}
          <div class="card p-5 rounded-lg bg-black/50 backdrop-blur-sm" style="transition-delay: {i * 100}ms">
            <div class="relative mb-4 overflow-hidden rounded-lg aspect-square">
              <img src={member.image} alt={member.name} class="w-full h-full object-cover grayscale hover:grayscale-0 transition-all duration-500">
              <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div>
              <div class="absolute bottom-0 left-0 w-full p-3">
                <h4 class="text-xl font-heading text-white mb-0">{member.name}</h4>
                <p class="text-accent-red text-sm">{member.role}</p>
              </div>
            </div>
            <p class="text-gray-400 text-sm">{member.bio}</p>
          </div>
        {/each}
      </div> -->
    </div>
  </div>
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>