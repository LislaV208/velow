<script lang="ts">
  import { onMount } from 'svelte';
  import Header from './lib/components/Header.svelte';
  import HomeSection from './lib/components/HomeSection.svelte';
  import AboutSection from './lib/components/AboutSection.svelte';
  import MusicSection from './lib/components/MusicSection.svelte';
  import ShowsSection from './lib/components/ShowsSection.svelte';
  import MediaSection from './lib/components/MediaSection.svelte';
  import MerchSection from './lib/components/MerchSection.svelte';
  // import SocialSection from './lib/components/SocialSection.svelte'; // Usunięte - linki społecznościowe przeniesione do sekcji kontaktowej
  import ContactSection from './lib/components/ContactSection.svelte';
  import Footer from './lib/components/Footer.svelte';
  
  // Stan ładowania czcionek
  let fontsLoaded = $state(false);
  
  onMount(() => {
    // Sprawdzenie, czy wszystkie czcionki zostały załadowane
    document.fonts.ready.then(() => {
      fontsLoaded = true;
    });
    
    // Fallback - jeśli czcionki są już załadowane
    if (document.fonts.status === 'loaded') {
      fontsLoaded = true;
    }
  });
</script>

<!-- Loader wyświetlany podczas ładowania czcionek -->
{#if !fontsLoaded}
  <div class="fixed inset-0 bg-black z-50 flex items-center justify-center">
    <div class="text-center">
      <div class="mt-4 flex justify-center">
        <div class="w-3 h-3 bg-white rounded-full mx-1 animate-pulse" style="animation-delay: 0ms"></div>
        <div class="w-3 h-3 bg-white rounded-full mx-1 animate-pulse" style="animation-delay: 200ms"></div>
        <div class="w-3 h-3 bg-white rounded-full mx-1 animate-pulse" style="animation-delay: 400ms"></div>
      </div>
    </div>
  </div>
{/if}

<!-- Główna zawartość strony - pojawi się po załadowaniu czcionek -->
<main class="transition-opacity duration-700 {fontsLoaded ? 'opacity-100' : 'opacity-0'}">
  <Header />
  <HomeSection />
  <AboutSection />
  <MusicSection />
  <ShowsSection />
  <!-- <MediaSection /> -->
  <MerchSection />
  <!-- <SocialSection /> --> <!-- Usunięte - linki społecznościowe przeniesione do sekcji kontaktowej -->
  <ContactSection />
  <Footer />
</main>