<script lang="ts">
  import { onMount } from 'svelte';
  
  let isVisible = $state(false);
  
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
      name: "Jan Kowalski",
      role: "Wokal / Gitara",
      image: "/images/member1.jpg",
      bio: "Założyciel zespołu, autor większości tekstów. Inspiruje się klasykami rocka lat 90."
    },
    {
      name: "Piotr Nowak",
      role: "Gitara prowadząca",
      image: "/images/member2.jpg",
      bio: "W zespole od 2018 roku. Wirtuoz gitary z klasycznym wykształceniem muzycznym."
    },
    {
      name: "Michał Wiśniewski",
      role: "Bas",
      image: "/images/member3.jpg",
      bio: "Odpowiedzialny za groove zespołu. Wcześniej grał w kilku undergroundowych projektach."
    },
    {
      name: "Tomasz Jankowski",
      role: "Perkusja",
      image: "/images/member4.jpg",
      bio: "Najmłodszy członek zespołu. Znany z energetycznych występów na żywo."
    }
  ];
</script>

<section id="about" class="section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-800 delay-50 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white">O Nas</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-10 mb-16">
        <div>
          <p class="text-gray-300 mb-6 text-lg">
            Velow to powstały w roku 2021 zespół, muzycznie będący 
w klimatach rocka alternatywnego. Po pierwszych, bardzo intensywnych
dwóch latach działalności, miało miejsce nasze pierwsze wyjście z mroku z 
naszym debiutanckim albumem pod tytułem “Wizje”,
który przyjął się bardzo dobrze w środowisku. Razem z premierą,
w 2023 wyruszyliśmy w trasę “Wizje Tour”, odwiedzając takie miasta jak
Szczecin, Gdańsk, Poznań. Nasza muzyka to pewna opowieść. 
To enigmatyczne teksty, które w połączeniu z energiczną
muzyką tworzą mieszankę wybuchową. 

          </p>
          <p class="text-gray-300 mb-6 text-lg">
            Mamy za sobą dwukrotny występ na Szczecińskich Juwenaliach, w naszej
dotychczasowej karierze graliśmy między innymi przed takimi zespołami
jak: Lady Pank, Kult, Enej, Organek

          </p>
          <p class="text-gray-300 text-md">
            "Jeśli takie są "Wizje" przyszłości polskiego rocka, to jest dobrze, 
naprawdę dobrze!" - EskaROCK
"Velow bywają i czadowi (przewrotna Smutna Piosenka), i refleksyjni 
(Mimo Strat, Miasto pełne krzyku). I w każdym wcieleniu im do twarzy"
 - TerazROCK

          </p>
          
          <div class="mt-8 inline-block">
            <a href="#music" class="btn border-accent-red text-accent-red hover:text-black">
              Posłuchaj naszej muzyki
            </a>
          </div>
        </div>
        <div class="relative">
          <div class="absolute -inset-4 bg-gradient-to-r from-accent-red to-transparent opacity-10 blur-lg"></div>
          <img src="/images/band-about.jpg" alt="Zespół Velow" class="w-full h-auto rounded-lg shadow-2xl relative z-10 grayscale hover:grayscale-0 transition-all duration-700">
          <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent rounded-lg"></div>
        </div>
      </div>
      
      <h3 class="text-3xl font-heading text-white mb-10 relative inline-block distortion-border pb-3">Członkowie zespołu</h3>
      
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
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
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>