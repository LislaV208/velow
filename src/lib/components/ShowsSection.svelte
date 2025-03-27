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
    
    const section = document.getElementById('shows');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
  
  const upcomingShows = [
    {
      date: "11.04.2025\n12.04.2025",
      venue: "Rampa - Kultura i Twierdza Design",
      city: "Goleniów",
      ticketLink: "https://www.facebook.com/events/3607994556164757",
      ticketText: "Wstęp free",
    },
    {
      date: "30.05.2025",
      venue: "Krzywy Gryf",
      city: "Szczecin",
      ticketLink: "https://ticketcore.org/bilety/2253/velow-godbite-wyjdzie-w-praniu.html",
      ticketText: "BILETY",
    },
    {
      date: "14.06.2025",
      venue: "Pan Gar",
      city: "Poznań",
      ticketLink: null,
      ticketText: "TBA",
    },
    {
      date: "TBA",
      venue: "Klub Mechanik",
      city: "Warszawa",
      ticketLink: null,
      ticketText: "TBA",
    },
    {
      date: "TBA",
      venue: "Green Club",
      city: "Gdańsk",
      ticketLink: null,
      ticketText: "TBA",
    },
    // {
    //   date: "18.11.2025",
    //   venue: "Klub Kwadrat",
    //   city: "Kraków",
    //   ticketLink: "https://example.com/tickets2"
    // },
    // {
    //   date: "25.11.2025",
    //   venue: "Klub B17",
    //   city: "Poznań",
    //   ticketLink: "https://example.com/tickets3"
    // },
    // {
    //   date: "02.12.2025",
    //   venue: "Klub Wytwórnia",
    //   city: "Łódź",
    //   ticketLink: "https://example.com/tickets4"
    // },
    // {
    //   date: "09.12.2025",
    //   venue: "Klub Parlament",
    //   city: "Gdańsk",
    //   ticketLink: "https://example.com/tickets5"
    // },
    // {
    //   date: "16.12.2025",
    //   venue: "Klub Rudy Kot",
    //   city: "Wrocław",
    //   ticketLink: "https://example.com/tickets6"
    // }
  ];
</script>

<!-- <section id="shows" class="section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative"> -->
<section id="shows" class="section py-20 relative">
  <!-- <div class="absolute inset-0 bg-cover bg-center opacity-50 grayscale" style="background-image: url('/images/live.webp')"></div> -->
  <div class="absolute inset-0 bg-cover bg-no-repeat bg-center opacity-0 sm:opacity-60 grayscale" style="background-image: url('/images/live.webp')"></div>
  <div class="absolute inset-0 bg-gradient-to-b from-black via-transparent to-black"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-800 delay-50 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="text-5xl! section-title text-white">Koncerty</h2>
      
      <div class="mb-10">
        <p class="text-white max-w-3xl text-lg">
          Sprawdź gdzie możesz nas zobaczyć na żywo w najbliższym czasie. Nasze koncerty to zawsze potężna dawka energii i niezapomniane wrażenia!
        </p>
      </div>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {#each upcomingShows as show, i}
          <div 
            class="card p-6 rounded-lg bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red flex flex-col h-full"
            style="transition-delay: {i * 100}ms"
          >
            <div class="flex justify-between mb-4">
              <div>
                <h3 class="text-2xl font-heading text-white group-hover:text-accent-red transition-colors">{show.city}</h3>
                <p class="text-accent">{show.venue}</p>
              </div>
              <div class="bg-gray-800 px-3 py-2 rounded relative overflow-hidden group-hover:bg-accent-red/20 transition-colors min-w-[100px] flex items-center justify-center">
                <span class="text-white font-medium relative z-10 text-center whitespace-pre-line">{show.date}</span>
              </div>
            </div>
            <div class="mt-auto pt-4 flex justify-end items-center">
              <a href={show.ticketLink} target="_blank" rel="noopener noreferrer" class="btn text-sm py-2 px-4 border-accent-red text-accent-red hover:text-black">{show.ticketText}</a>
            </div>
          </div>
        {/each}
      </div>
      
      <div class="mt-12 text-center">
        <div class="relative inline-block group">
          <a href="#contact" class="btn border-accent-red text-accent-red hover:text-black">Zabookuj koncert</a>
          <div class="absolute -inset-0.5 bg-accent-red opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
        </div>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>