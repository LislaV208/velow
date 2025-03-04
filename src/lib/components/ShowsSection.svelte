<script lang="ts">
  import { onMount } from 'svelte';
  
  let isVisible = $state(false);
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVisible = true;
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
      date: "12.11.2025",
      venue: "Klub Stodoła",
      city: "Warszawa",
      ticketLink: "https://example.com/tickets1"
    },
    {
      date: "18.11.2025",
      venue: "Klub Kwadrat",
      city: "Kraków",
      ticketLink: "https://example.com/tickets2"
    },
    {
      date: "25.11.2025",
      venue: "Klub B17",
      city: "Poznań",
      ticketLink: "https://example.com/tickets3"
    },
    {
      date: "02.12.2025",
      venue: "Klub Wytwórnia",
      city: "Łódź",
      ticketLink: "https://example.com/tickets4"
    },
    {
      date: "09.12.2025",
      venue: "Klub Parlament",
      city: "Gdańsk",
      ticketLink: "https://example.com/tickets5"
    },
    {
      date: "16.12.2025",
      venue: "Klub Rudy Kot",
      city: "Wrocław",
      ticketLink: "https://example.com/tickets6"
    }
  ];
</script>

<section id="shows" class="section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-1000 delay-300 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white">Koncerty</h2>
      
      <div class="mb-10">
        <p class="text-gray-300 max-w-3xl text-lg">
          Sprawdź gdzie możesz nas zobaczyć na żywo w najbliższym czasie. Nasze koncerty to zawsze potężna dawka energii i niezapomniane wrażenia!
        </p>
      </div>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {#each upcomingShows as show, i}
          <div 
            class="card p-6 rounded-lg bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
            style="transition-delay: {i * 100}ms"
          >
            <div class="flex justify-between items-start mb-4">
              <div>
                <h3 class="text-2xl font-heading text-white group-hover:text-accent-red transition-colors">{show.city}</h3>
                <p class="text-accent">{show.venue}</p>
              </div>
              <div class="bg-gray-800 px-3 py-2 rounded relative overflow-hidden group-hover:bg-accent-red/20 transition-colors">
                <span class="text-white font-medium relative z-10">{show.date}</span>
              </div>
            </div>
            <div class="mt-auto pt-4 flex justify-between items-center">
              <span class="text-gray-400 text-sm">20:00</span>
              <a href={show.ticketLink} target="_blank" rel="noopener noreferrer" class="btn text-sm py-2 px-4 border-accent-red text-accent-red hover:text-black">Bilety</a>
            </div>
          </div>
        {/each}
      </div>
      
      <div class="mt-12 text-center">
        <div class="relative inline-block group">
          <a href="mailto:koncerty@velow.pl" class="btn border-accent-red text-accent-red hover:text-black">Zaproś nas na koncert</a>
          <div class="absolute -inset-0.5 bg-accent-red opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
        </div>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>