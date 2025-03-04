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
    
    const section = document.getElementById('social');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
  
  const socialLinks = [
    { 
      name: "Facebook", 
      url: "https://facebook.com", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
            </svg>` 
    },
    { 
      name: "Instagram", 
      url: "https://instagram.com", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd" />
            </svg>` 
    },
    { 
      name: "YouTube", 
      url: "https://youtube.com", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M19.812 5.418c.861.23 1.538.907 1.768 1.768C21.998 8.746 22 12 22 12s0 3.255-.418 4.814a2.504 2.504 0 0 1-1.768 1.768c-1.56.419-7.814.419-7.814.419s-6.255 0-7.814-.419a2.505 2.505 0 0 1-1.768-1.768C2 15.255 2 12 2 12s0-3.255.417-4.814a2.507 2.507 0 0 1 1.768-1.768C5.744 5 11.998 5 11.998 5s6.255 0 7.814.418ZM15.194 12 10 15V9l5.194 3Z" clip-rule="evenodd" />
            </svg>` 
    },
    { 
      name: "Spotify", 
      url: "https://spotify.com", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/>
            </svg>` 
    },
    { 
      name: "Apple Music", 
      url: "https://music.apple.com", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M23.997 6.124c0-.738-.065-1.47-.24-2.19-.317-1.31-1.062-2.31-2.18-3.043C21.003.517 20.373.285 19.7.164c-.517-.093-1.038-.135-1.564-.15-.04-.003-.083-.01-.124-.013H5.988c-.152.01-.303.017-.455.026C4.786.07 4.043.15 3.34.428 2.004.958 1.04 1.88.448 3.208c-.207.51-.332 1.04-.39 1.58C.017 5.03 0 5.27 0 5.51v12.98c0 .23.016.46.05.69.06.55.182 1.07.4 1.58.61 1.35 1.6 2.27 2.95 2.79.65.25 1.34.32 2.03.36.35.02.7.03 1.06.03h12.9c.386 0 .77-.01 1.15-.04.673-.05 1.34-.14 1.985-.38 1.36-.52 2.33-1.45 2.93-2.8.16-.33.28-.67.36-1.02.05-.2.08-.41.08-.63v-13.2c-.003-.295-.04-.59-.093-.87zm-12.583 12.12c-.137.141-.31.21-.49.21-.368-.004-.66-.31-.658-.67.002-.36.296-.65.655-.65.363.004.65.302.65.666-.003.192-.07.36-.19.495l.032-.05zm8.944-3.935c-.037.2-.07.4-.104.602-.07.428-.198.833-.395 1.2-.38.7-.936 1.136-1.673 1.22-.54.063-1.076.04-1.615.115-.468.066-.94.044-1.413.044h-5.44l.016-.776c.004-.2-.03-.4-.03-.6v-10.9c0-.11.014-.22.03-.33.01-.08.03-.15.04-.23.1-.72.62-1.38 1.33-1.55.14-.03.28-.05.42-.05l.08-.01h7.14c.1.01.21.02.31.04.5.09.99.32 1.25.8.26.47.35.99.35 1.53v4.24c0 .04-.01.07-.01.11-.04 1.43-.01 2.86-.04 4.29zm-11.98-12.99c-.03.077-.073.143-.13.2-.29.297-.72.37-1.08.18-.36-.19-.54-.58-.42-.98.12-.4.53-.65.94-.57.54.11.83.72.52 1.17h.17zm15.52 2.53c-.21.026-.43.037-.65.037L10.39 3.9l.2-.98h8.24c.97 0 1.38.41 1.44 1.38.01.17.01.34.01.51v.11c-.1.07-.01.14-.01.22l-.01.14c-.07.28-.21.52-.47.65z"/>
            </svg>` 
    },
    { 
      name: "Bandcamp", 
      url: "https://bandcamp.com", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M0 18.75l7.437-13.5H24l-7.438 13.5H0z"/>
            </svg>` 
    }
  ];
</script>

<section id="social" class="section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 text-center relative z-10">
    <div class={`transition-all duration-1000 delay-300 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white mx-auto">Obserwuj nas</h2>
      
      <p class="text-gray-300 max-w-2xl mx-auto mb-12 text-lg">
        Bądź na bieżąco z naszymi nowościami, koncertami i zakulisowymi materiałami. Obserwuj nas w mediach społecznościowych!
      </p>
      
      <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-8">
        {#each socialLinks as link, i}
          <a 
            href={link.url} 
            target="_blank" 
            rel="noopener noreferrer" 
            class="flex flex-col items-center justify-center p-6 rounded-lg bg-black/50 backdrop-blur-sm border border-gray-800 hover:border-accent-silver transition-all duration-300 transform hover:-translate-y-2 group"
            style="transition-delay: {i * 100}ms"
          >
            <div class="text-gray-400 group-hover:text-accent-silver transition-colors mb-3">
              {@html link.icon}
            </div>
            <span class="text-white font-medium">{link.name}</span>
          </a>
        {/each}
      </div>
      
      <div class="mt-16">
        <p class="text-gray-300 mb-6">Dołącz do naszej społeczności i bądź pierwszym, który usłyszy o nowych wydawnictwach i koncertach!</p>
        <div class="relative inline-block group">
          <a href="#contact" class="btn border-accent-silver text-accent-silver hover:text-black">Zapisz się na newsletter</a>
          <div class="absolute -inset-0.5 bg-accent-steel opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
        </div>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>