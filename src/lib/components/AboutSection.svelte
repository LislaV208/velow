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
    <div class={`transition-all duration-1000 delay-300 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white">O Nas</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-10 mb-16">
        <div>
          <p class="text-gray-300 mb-6 text-lg">
            Velow to polski zespół rockowy założony w 2017 roku w Warszawie. Nasza muzyka to połączenie surowej energii rocka alternatywnego z melodyjnymi kompozycjami i tekstami, które opowiadają o życiowych doświadczeniach, emocjach i społecznych obserwacjach.
          </p>
          <p class="text-gray-300 mb-6 text-lg">
            Przez lata koncertowaliśmy w całej Polsce, dzieląc scenę z wieloma uznanymi artystami. Nasz debiutancki album <span class="text-accent-red font-semibold">"Pierwszy Krok"</span> został wydany w 2022 roku i spotkał się z ciepłym przyjęciem zarówno fanów, jak i krytyków.
          </p>
          <p class="text-gray-300 text-lg">
            Obecnie pracujemy nad nowym materiałem, który będzie jeszcze bardziej dojrzały i zróżnicowany. Nasze występy na żywo to zawsze gwarancja potężnego brzmienia i niezapomnianej energii.
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