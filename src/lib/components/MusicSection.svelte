<script lang="ts">
  import { onMount } from 'svelte';
  
  const albumTracks = [
    { title: "Pierwszy Krok", duration: "3:45", isHighlighted: true },
    { title: "Ciemna Strona", duration: "4:12", isHighlighted: false },
    { title: "Bez Odwrotu", duration: "3:58", isHighlighted: false },
    { title: "Światła Miasta", duration: "5:21", isHighlighted: false },
    { title: "Ostatni Raz", duration: "4:05", isHighlighted: false },
    { title: "Nowy Dzień", duration: "3:37", isHighlighted: false },
    { title: "Poza Kontrolą", duration: "4:42", isHighlighted: false },
    { title: "Granice", duration: "3:51", isHighlighted: false },
    { title: "Wieczny Ogień", duration: "5:03", isHighlighted: false },
    { title: "Powrót", duration: "4:28", isHighlighted: false }
  ];
  
  let isVisible = $state(false);
  let activeTrack = $state(0);
  
  function setActiveTrack(index) {
    activeTrack = index;
  }
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVisible = true;
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

<section id="music" class="section bg-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-1000 delay-300 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white">Muzyka</h2>
      
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
        <div>
          <div class="relative mb-8 group">
            <div class="absolute -inset-4 bg-gradient-to-r from-accent-silver to-transparent opacity-0 group-hover:opacity-20 blur-lg transition-opacity duration-700"></div>
            <img src="/images/album-cover.jpg" alt="Album Pierwszy Krok" class="w-full h-auto rounded-lg shadow-2xl relative z-10">
            <div class="absolute inset-0 bg-gradient-to-t from-black/90 to-transparent/30 rounded-lg"></div>
            <div class="absolute bottom-0 left-0 p-6">
              <h3 class="text-3xl font-heading text-white">Pierwszy Krok</h3>
              <p class="text-accent-silver">Album (2022)</p>
            </div>
          </div>
          
          <div class="flex flex-wrap gap-4 mb-8">
            <a href="https://open.spotify.com/artist/" target="_blank" rel="noopener noreferrer" class="btn border-accent-silver text-accent-silver hover:text-black">
              <span class="flex items-center">
                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/>
                </svg>
                Spotify
              </span>
            </a>
            <a href="https://youtube.com/channel/" target="_blank" rel="noopener noreferrer" class="btn">
              <span class="flex items-center">
                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/>
                </svg>
                YouTube
              </span>
            </a>
            <a href="https://music.apple.com/artist/" target="_blank" rel="noopener noreferrer" class="btn">
              <span class="flex items-center">
                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M23.997 6.124c0-.738-.065-1.47-.24-2.19-.317-1.31-1.062-2.31-2.18-3.043C21.003.517 20.373.285 19.7.164c-.517-.093-1.038-.135-1.564-.15-.04-.003-.083-.01-.124-.013H5.988c-.152.01-.303.017-.455.026C4.786.07 4.043.15 3.34.428 2.004.958 1.04 1.88.448 3.208c-.207.51-.332 1.04-.39 1.58C.017 5.03 0 5.27 0 5.51v12.98c0 .23.016.46.05.69.06.55.182 1.07.4 1.58.61 1.35 1.6 2.27 2.95 2.79.65.25 1.34.32 2.03.36.35.02.7.03 1.06.03h12.9c.386 0 .77-.01 1.15-.04.673-.05 1.34-.14 1.985-.38 1.36-.52 2.33-1.45 2.93-2.8.16-.33.28-.67.36-1.02.05-.2.08-.41.08-.63v-13.2c-.003-.295-.04-.59-.093-.87zm-12.583 12.12c-.137.141-.31.21-.49.21-.368-.004-.66-.31-.658-.67.002-.36.296-.65.655-.65.363.004.65.302.65.666-.003.192-.07.36-.19.495l.032-.05zm8.944-3.935c-.037.2-.07.4-.104.602-.07.428-.198.833-.395 1.2-.38.7-.936 1.136-1.673 1.22-.54.063-1.076.04-1.615.115-.468.066-.94.044-1.413.044h-5.44l.016-.776c.004-.2-.03-.4-.03-.6v-10.9c0-.11.014-.22.03-.33.01-.08.03-.15.04-.23.1-.72.62-1.38 1.33-1.55.14-.03.28-.05.42-.05l.08-.01h7.14c.1.01.21.02.31.04.5.09.99.32 1.25.8.26.47.35.99.35 1.53v4.24c0 .04-.01.07-.01.11-.04 1.43-.01 2.86-.04 4.29zm-11.98-12.99c-.03.077-.073.143-.13.2-.29.297-.72.37-1.08.18-.36-.19-.54-.58-.42-.98.12-.4.53-.65.94-.57.54.11.83.72.52 1.17h.17zm15.52 2.53c-.21.026-.43.037-.65.037L10.39 3.9l.2-.98h8.24c.97 0 1.38.41 1.44 1.38.01.17.01.34.01.51v.11c-.1.07-.01.14-.01.22l-.01.14c-.07.28-.21.52-.47.65z"/>
                </svg>
                Apple Music
              </span>
            </a>
          </div>
          
          <div class="bg-gray-900/50 backdrop-blur-sm p-6 rounded-lg border border-gray-800">
            <h4 class="text-xl font-heading text-white mb-4">Posłuchaj na Spotify</h4>
            <div class="aspect-video">
              <iframe src="https://open.spotify.com/embed/album/placeholder" width="100%" height="100%" frameborder="0" allowtransparency="true" allow="encrypted-media" title="Spotify Embed"></iframe>
            </div>
          </div>
        </div>
        
        <div>
          <h3 class="text-3xl font-heading text-white mb-6 relative inline-block distortion-border pb-3">Lista utworów</h3>
          
          <div class="space-y-4">
            {#each albumTracks as track, i}
              <div 
                class={`p-4 rounded-lg transition-all duration-300 cursor-pointer ${i === activeTrack ? 'bg-accent-silver/20 border-l-4 border-accent-silver' : 'bg-gray-900/50 hover:bg-gray-800/50'}`}
                onclick={() => setActiveTrack(i)}
                onkeydown={(e) => e.key === 'Enter' && setActiveTrack(i)}
                tabindex="0"
                role="button"
              >
                <div class="flex justify-between items-center">
                  <div class="flex items-center">
                    <span class={`text-2xl mr-4 font-heading ${i === activeTrack ? 'text-accent-silver' : 'text-gray-500'}`}>{i + 1}</span>
                    <div>
                      <h4 class="text-white font-medium">{track.title}</h4>
                      {#if track.isHighlighted}
                        <span class="text-xs text-accent-silver mt-1 inline-block">Singiel</span>
                      {/if}
                    </div>
                  </div>
                  <div class="flex items-center">
                    <span class="text-gray-400 mr-4">{track.duration}</span>
                    <div class="flex space-x-2">
                      <a href="https://open.spotify.com/track/placeholder" target="_blank" rel="noopener noreferrer" class="text-gray-400 hover:text-accent-silver transition-colors">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                          <path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/>
                        </svg>
                      </a>
                      <a href="https://youtube.com/watch?v=placeholder" target="_blank" rel="noopener noreferrer" class="text-gray-400 hover:text-accent-silver transition-colors">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                          <path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/>
                        </svg>
                      </a>
                    </div>
                  </div>
                </div>
              </div>
            {/each}
          </div>
          
          <div class={`mt-10 transition-all duration-1000 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
            <h3 class="text-3xl font-heading text-white mb-6 relative inline-block distortion-border pb-3">Najnowszy singiel</h3>
            <div class="bg-gray-900/50 backdrop-blur-sm p-6 rounded-lg border border-gray-800 relative group">
              <div class="absolute -inset-0.5 bg-gradient-to-r from-accent-silver to-transparent opacity-0 group-hover:opacity-20 blur-sm transition-opacity duration-700"></div>
              <div class="aspect-video relative z-10">
                <iframe width="100%" height="100%" src="https://www.youtube.com/embed/placeholder" title="Velow - Pierwszy Krok (Official Video)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>