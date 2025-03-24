<script lang="ts">
  import { onMount } from 'svelte';
  
  const albumTracks = [
    { title: "Intro", duration: "1:05",  },
    { title: "Mimo Strat", duration: "4:05",  },
    { title: "Nietykalna", duration: "4:06",  },
    { title: "Miasto Pełne Krzyku", duration: "5:44",  },
    { title: "Wizje", duration: "3:39",  },
    { title: "Smutna Piosenka", duration: "3:04",  },
    { title: "Omamiony", duration: "4:00",  },
    { title: "Paranoja", duration: "4:14",  },
    { title: "Ostatni", duration: "4:23",  },
    
  ];
  
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
    
    const section = document.getElementById('music');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
</script>

<section id="music" class="section bg-black relative">
  <!-- <div class="absolute inset-0 bg-noise-pattern opacity-10"></div> -->
  <div class="absolute inset-0 bg-cover bg-center opacity-50" style="background-image: url('/images/wizje_tlo.webp')"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  <div class="absolute inset-0 bg-gradient-to-b from-black/70 via-transparent to-black/70"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-800 delay-50 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <!-- <div> -->
        
      <!-- </div> -->
      
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
        <div>
          <h2 class="text-5xl! section-title text-white">Muzyka</h2>
        <!-- <div class="relative mb-8 group">
            <div class="absolute -inset-4 bg-gradient-to-r from-accent-silver to-transparent opacity-0 group-hover:opacity-20 blur-lg transition-opacity duration-700"></div>
            <img src="/images/album-cover.webp" alt="Album Pierwszy Krok" class="w-full h-auto rounded-lg shadow-2xl relative z-10">
            <div class="absolute inset-0 bg-gradient-to-t from-black/90 to-transparent/30 rounded-lg"></div>
            
          </div> -->
          
          
          
          <div 
            class="mx-auto card p-4 rounded-lg bg-black/50 backdrop-blur-sm max-w-[450px] transition-all duration-300 hover:scale-[1.02] hover:shadow-lg hover:shadow-accent-silver/20 group relative"
            role="button"
            tabindex="0"
            aria-label="Otwórz album Wizje"
            onkeydown={(e) => e.key === 'Enter' && console.log('Album clicked')}
            onclick={() => console.log('Album clicked')}
          >
            <div class="relative overflow-hidden rounded-lg">
              <img src="/images/okladka.webp" alt="Velow - Wizje" class="w-full h-auto object-contain max-h-[400px] transition-transform duration-500 group-hover:scale-[1.03]">
              <!-- <div class="bg-black/60 absolute bottom-0 left-0 right-0 w-full py-2 text-center transition-all duration-300 opacity-0 group-hover:opacity-100">
                <span class="text-white font-md">O albumie...</span>
              </div> -->
              <!-- <div class="absolute bottom-0 left-0 right-0 bg-black/70 backdrop-blur-sm p-3">
                <h3 class="text-accent-silver font-heading text-xl group-hover:text-white transition-colors duration-300 text-center">Wizje (2023)</h3>
              </div> -->
            </div>
            <!-- Removing the duplicate title that was below the image -->
            <div class="text-center mt-4">
              <h3 class="text-accent-silver font-heading text-xl group-hover:text-white transition-colors duration-300">Wizje (2023)</h3>
            </div>
          </div>
        </div>

        
        <div>
          <!-- <h2 class="text-5xl! section-title text-white">Posłuchaj</h2> -->
          
          <div class="space-y-3">
            {#each albumTracks as track, i}
              <div 
                class="px-4 py-3 rounded-lg transition-all duration-300 bg-gray-900/50 hover:bg-gray-800/80"
                tabindex="0"
                role="button"
              >
                <div class="flex justify-between items-center">
                  <div class="flex items-center">
                    <span class="text-2xl mr-4 font-heading text-gray-500">{i + 1}</span>
                    <div>
                      <h4 class="text-lg! text-white">{track.title}</h4>
                      <!-- {#if track.isHighlighted}
                        <span class="text-xs text-accent-silver mt-1 inline-block">Singiel</span>
                      {/if} -->
                    </div>
                  </div>
                  <div class="flex items-center">
                    <span class="text-gray-400 mr-4">{track.duration}</span>
                    <!-- <div class="flex space-x-2">
                      <button 
                        class="text-gray-400 cursor-pointer hover:text-accent-silver transition-colors focus:outline-none" 
                        aria-label="Odtwórz {track.title}"
                        onclick={() => console.log(`Playing track: ${track.title}`)}
                      >
                        <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                          <circle cx="12" cy="12" r="10" fill="currentColor"/>
                          <path d="M10 8v8l6-4z" fill="black"/>
                        </svg>
                      </button>
                    </div> -->
                  </div>
                </div>
              </div>
            {/each}
          </div>

          
          
          <!-- <div class={`mt-10 transition-all duration-1000 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
            <h3 class="text-3xl font-heading text-white mb-6 relative inline-block distortion-border pb-3">Najnowszy singiel</h3>
            <div class="bg-gray-900/50 backdrop-blur-sm p-6 rounded-lg border border-gray-800 relative group">
              <div class="absolute -inset-0.5 bg-gradient-to-r from-accent-silver to-transparent opacity-0 group-hover:opacity-20 blur-sm transition-opacity duration-700"></div>
              <div class="aspect-video relative z-10">
                <iframe width="100%" height="100%" src="https://www.youtube.com/embed/placeholder" title="Velow - Pierwszy Krok (Official Video)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
              </div>
            </div>
          </div> -->
        </div>
      </div>
      <div class="flex flex-wrap justify-center gap-3 mt-8">
        <a href="https://open.spotify.com/artist/350Cbr6kdjvcgWsYZMdIL1" target="_blank" rel="noopener noreferrer" class="btn">
          <span class="flex items-center justify-center text-sm w-[150px]">
            <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/>
            </svg>
            Spotify
          </span>
        </a>
        <a href="https://www.youtube.com/playlist?list=PLWAqjoney6vN6Ts7zi1UBqwud6UbokzZY" target="_blank" rel="noopener noreferrer" class="btn">
          <span class="flex items-center justify-center text-sm w-[150px]">
            <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
              <path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/>
            </svg>
            YouTube
          </span>
        </a>
        <a href="https://music.apple.com/pl/album/wizje/1681105188" target="_blank" rel="noopener noreferrer" class="btn">
          <span class="flex items-center justify-center text-sm w-[150px]">
            <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
              <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/>
            </svg>
            Apple Music
          </span>
        </a>
        <a href="https://tidal.com/browse/album/287470814" target="_blank" rel="noopener noreferrer" class="btn">
          <span class="flex items-center justify-center text-sm w-[150px]">
            <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12.012 3.992L8.008 7.996 4.004 3.992 0 7.996 4.004 12l4.004-4.004L12.012 12l-4.004 4.004 4.004 4.004 4.004-4.004L12.012 12l4.004-4.004-4.004-4.004zM16.042 7.996l3.979-3.979L24 7.996l-3.979 3.979z"/>
            </svg>
            TIDAL
          </span>
        </a>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>