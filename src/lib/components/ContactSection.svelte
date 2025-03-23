<script lang="ts">
  import { preventDefault } from 'svelte/legacy';
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
    
    const section = document.getElementById('contact');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
  
  let name = $state('');
  let email = $state('');
  let message = $state('');
  let submitted = $state(false);
  
  function handleSubmit() {
    // In a real application, you would send the form data to a server
    console.log({ name, email, message });
    submitted = true;
    
    // Reset form after submission
    setTimeout(() => {
      name = '';
      email = '';
      message = '';
      submitted = false;
    }, 3000);
  }
  
  // Dodane linki społecznościowe
  const socialLinks = [
    { 
      name: "Facebook", 
      url: "https://www.facebook.com/thevelowband/", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
            </svg>` 
    },
    { 
      name: "Instagram", 
      url: "https://www.instagram.com/the.velow/", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd" />
            </svg>` 
    },
    { 
      name: "TikTok", 
      url: "https://www.tiktok.com/@velowband", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24"><path d="M19.589 6.686a4.793 4.793 0 0 1-3.77-4.245V2h-3.445v13.672a2.896 2.896 0 0 1-5.201 1.743l-.002-.001.002.001a2.895 2.895 0 0 1 3.183-4.51v-3.5a6.329 6.329 0 0 0-5.394 10.692 6.33 6.33 0 0 0 10.857-4.424V8.687a8.182 8.182 0 0 0 4.773 1.526V6.79a4.831 4.831 0 0 1-1.003-.104z"/></svg>` 
    },
    { 
      name: "YouTube", 
      url: "https://www.youtube.com/channel/UC6nMbMtz8kkosGCxD1jTzBg", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M19.812 5.418c.861.23 1.538.907 1.768 1.768C21.998 8.746 22 12 22 12s0 3.255-.418 4.814a2.504 2.504 0 0 1-1.768 1.768c-1.56.419-7.814.419-7.814.419s-6.255 0-7.814-.419a2.505 2.505 0 0 1-1.768-1.768C2 15.255 2 12 2 12s0-3.255.417-4.814a2.507 2.507 0 0 1 1.768-1.768C5.744 5 11.998 5 11.998 5s6.255 0 7.814.418ZM15.194 12 10 15V9l5.194 3Z" clip-rule="evenodd" />
            </svg>` 
    },
    { 
      name: "Spotify", 
      url: "https://open.spotify.com/artist/350Cbr6kdjvcgWsYZMdIL1", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/>
            </svg>` 
    },
    { 
      name: "Apple Music", 
      url: "https://music.apple.com/pl/artist/velow/1749972254", 
      icon: `<svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24">
              <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/>
            </svg>` 
    },
    
  ];
</script>

<section id="contact" class="section bg-black relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-1000 delay-300 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
        <div>
          <h2 class="section-title text-white">Kontakt</h2>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <!-- Lewa kolumna -->
            <div class="space-y-8">
              <!-- Telefon -->
              <div class="flex items-start group hover:scale-105 transition-transform duration-300 h-[85px]">
                <div class="mr-4 text-accent-red flex-shrink-0 w-8 flex justify-center">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-white font-medium text-lg mb-1">Telefon</h3>
                  <a href="tel:+48664082748" class="text-gray-300 hover:text-accent-red transition-colors block">+48 664 082 748</a>
                  <p class="text-gray-400 text-sm mt-1">Kontakt: Tomasz Guz</p>
                </div>
              </div>
              
              <!-- Email ogólny -->
              <div class="flex items-start group hover:scale-105 transition-transform duration-300 h-[85px]">
                <div class="mr-4 text-accent-red flex-shrink-0 w-8 flex justify-center">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-white font-medium text-lg mb-1">Email ogólny</h3>
                  <a href="mailto:kontakt@velow.pl" class="text-gray-300 hover:text-accent-red transition-colors block">kontakt@velow.pl</a>
                  <p class="text-gray-400 text-sm mt-1 opacity-0">Placeholder</p>
                </div>
              </div>
            </div>
            
            <!-- Prawa kolumna -->
            <div class="space-y-8">
              <!-- Email merch -->
              <div class="flex items-start group hover:scale-105 transition-transform duration-300 h-[85px]">
                <div class="mr-4 text-accent-red flex-shrink-0 w-8 flex justify-center">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-white font-medium text-lg mb-1">Zamówienia merchu</h3>
                  <a href="mailto:merch@velow.pl" class="text-gray-300 hover:text-accent-red transition-colors block">merch@velow.pl</a>
                  <p class="text-gray-400 text-sm mt-1 opacity-0">Placeholder</p>
                </div>
              </div>
              
              <!-- Booking -->
              <div class="flex items-start group hover:scale-105 transition-transform duration-300 h-[85px]">
                <div class="mr-4 text-accent-red flex-shrink-0 w-8 flex justify-center">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-white font-medium text-lg mb-1">Booking koncertów</h3>
                  <a href="mailto:booking@velow.pl" class="text-gray-300 hover:text-accent-red transition-colors block">booking@velow.pl</a>
                  <p class="text-gray-400 text-sm mt-1 opacity-0">Placeholder</p>
                </div>
              </div>
            </div>
          </div>
          
          
        </div>
        
        <!-- Sekcja z linkami społecznościowymi -->
        <div>
          <h2 class="section-title text-white">Obserwuj nas</h2>
          <p class="text-gray-300 mb-8">
            Bądź na bieżąco z naszymi nowościami, koncertami i zakulisowymi materiałami.
          </p>
          
          <div class="grid grid-cols-2 sm:grid-cols-3 gap-4">
            {#each socialLinks as link, i}
              <a 
                href={link.url} 
                target="_blank" 
                rel="noopener noreferrer" 
                class="flex flex-col items-center justify-center p-4 rounded-lg bg-black/50 backdrop-blur-sm border border-gray-800 hover:border-accent-silver transition-all duration-300 transform hover:-translate-y-1 group"
                style="transition-delay: {i * 100}ms"
              >
                <div class="text-gray-400 group-hover:text-accent-silver transition-colors mb-2" aria-hidden="true">
                  {@html link.icon}
                </div>
                <span class="text-sm text-gray-300 group-hover:text-white transition-colors">{link.name}</span>
              </a>
            {/each}
          </div>
        </div>
        
        
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>