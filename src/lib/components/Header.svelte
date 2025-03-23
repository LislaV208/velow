<script lang="ts">
  import { onMount } from 'svelte';
  
  let scrollY: number;
  let isScrolled = $state(false);
  let isVisible = $state(false);
  let isMobileMenuOpen = $state(false);
  let menuRef: HTMLElement;
  let buttonRef: HTMLElement;
  let currentSection = $state('home');
  let indicatorLeft = $state(0);
  let indicatorWidth = $state(0);
  let navListRef: HTMLUListElement;
  let mobileNavListRef: HTMLUListElement;
  let mobileIndicatorTop = $state(0);
  let mobileIndicatorWidth = $state(0);
  
  // Referencje do linków nawigacyjnych
  let navLinks: Record<string, HTMLAnchorElement | null> = {};
  let mobileNavLinks: Record<string, HTMLAnchorElement | null> = {};
  
  // Lista wszystkich sekcji strony
  const sections = ['home', 'about', 'music', 'shows', 'merch', 'contact'];
  
  // Inicjalizacja obiektu navLinks i mobileNavLinks
  sections.forEach(section => {
    if (section !== 'home') {
      navLinks[section] = null;
      mobileNavLinks[section] = null;
    }
  });
  
  onMount(() => {
    const handleScroll = () => {
      scrollY = window.scrollY;
      // console.log('scrollY: ' + scrollY + 'px');
      // isScrolled = scrollY > 777;
      isScrolled = true;
      isVisible = scrollY > window.innerHeight * 0.88; 
      
      // Sprawdzanie, która sekcja jest aktualnie widoczna
      updateCurrentSection();
    };
    
    // Funkcja do określania aktualnie widocznej sekcji
    const updateCurrentSection = () => {
      // Odwracamy listę sekcji, aby sprawdzać od dołu strony (zapobiega problemom z nakładającymi się sekcjami)
      const sectionsToCheck = [...sections].reverse();
      
      for (const section of sectionsToCheck) {
        const element = document.getElementById(section);
        if (element) {
          const rect = element.getBoundingClientRect();
          // Jeśli górna krawędź sekcji jest w widoku lub tuż nad nim (do 100px)
          if (rect.top <= 100 && rect.bottom > 0) {
            if (currentSection !== section) {
              currentSection = section;
              updateIndicator();
            }
            break;
          }
        }
      }
    };
    
    window.addEventListener('scroll', handleScroll);
    document.addEventListener('click', handleClickOutside);
    
    // Wywołaj raz na początku, aby ustawić początkową sekcję
    setTimeout(() => {
      updateCurrentSection();
      updateIndicator();
    }, 100);
    
    return () => {
      window.removeEventListener('scroll', handleScroll);
      document.removeEventListener('click', handleClickOutside);
    };
  });
  
  const handleClickOutside = (event: MouseEvent) => {
    if (isMobileMenuOpen && menuRef && buttonRef) {
      const target = event.target as Node;
      if (!menuRef.contains(target) && !buttonRef.contains(target)) {
        closeMobileMenu();
      }
    }
  };
  
  function toggleMobileMenu(): void {
    isMobileMenuOpen = !isMobileMenuOpen;
  }
  
  function closeMobileMenu(): void {
    isMobileMenuOpen = false;
  }
  
  // Funkcja sprawdzająca, czy dany link jest aktywny
  function isActive(section: string): boolean {
    return currentSection === section;
  }
  
  // Funkcja aktualizująca pozycję i szerokość wskaźnika
  function updateIndicator() {
    if (currentSection === 'home') {
      // Gdy jesteśmy na stronie głównej, ukrywamy wskaźnik
      indicatorWidth = 0;
      mobileIndicatorWidth = 0;
      return;
    }
    
    // Aktualizacja wskaźnika dla widoku desktopowego
    const activeLink = navLinks[currentSection];
    if (activeLink && navListRef) {
      const linkRect = activeLink.getBoundingClientRect();
      const navRect = navListRef.getBoundingClientRect();
      
      // Obliczamy pozycję względem kontenera nawigacji
      indicatorLeft = linkRect.left - navRect.left;
      indicatorWidth = linkRect.width;
    }
    
    // Aktualizacja wskaźnika dla widoku mobilnego
    const activeMobileLink = mobileNavLinks[currentSection];
    if (activeMobileLink && mobileNavListRef) {
      const linkRect = activeMobileLink.getBoundingClientRect();
      const navRect = mobileNavListRef.getBoundingClientRect();
      
      // Obliczamy pozycję względem kontenera nawigacji
      mobileIndicatorTop = linkRect.top - navRect.top + linkRect.height;
      mobileIndicatorWidth = linkRect.width;
    }
  }
</script>

<header class={`fixed top-0 left-0 w-full z-50 transition-all duration-200 ${isScrolled ? 'bg-black border-2 border-black border-b-white/20 py-5' : 'bg-transparent'} ${isVisible ? 'translate-y-0' : '-translate-y-full'}`}>
  <div class="container mx-auto px-4 flex justify-between items-center">
    <a href="#home" class="text-white text-3xl font-bold relative tracking-wider overflow-visible group">
      <h1 class="relative z-10 inline-block transition-transform duration-300 group-hover:scale-110" style="font-family: 'BluPurpl', sans-serif !important; text-transform: none;">veLOw</h1>
      <span class="absolute bottom-0 left-0 w-full h-0.5 bg-accent-silver transform scale-x-0 transition-transform duration-300 group-hover:scale-x-100"></span>
    </a>
    
    <nav class="hidden md:block">
      <div class="nav-container relative">
        <ul class="flex space-x-8" bind:this={navListRef}>
          <li><a href="#about" class="nav-link text-white hover:text-accent-silver text-2xl" bind:this={navLinks['about']}>O Nas</a></li>
          <li><a href="#music" class="nav-link text-white hover:text-accent-silver text-2xl" bind:this={navLinks['music']}>Muzyka</a></li>
          <li><a href="#shows" class="nav-link text-white hover:text-accent-silver text-2xl" bind:this={navLinks['shows']}>Koncerty</a></li>
          <!-- <li><a href="#media" class="nav-link text-white hover:text-accent-silver">Media</a></li> -->
          <li><a href="#merch" class="nav-link text-white hover:text-accent-silver text-2xl" bind:this={navLinks['merch']}>Merch</a></li>
          <li><a href="#contact" class="nav-link text-white hover:text-accent-silver text-2xl" bind:this={navLinks['contact']}>Kontakt</a></li>
        </ul>
        <span class="nav-indicator" style="left: {indicatorLeft}px; width: {indicatorWidth}px;"></span>
      </div>
    </nav>
    
    <button 
      class="md:hidden text-white relative z-10 w-10 h-10 flex items-center justify-center" 
      aria-label="Menu"
      onclick={() => toggleMobileMenu()}
      bind:this={buttonRef}
    >
      <div class="w-6 flex flex-col items-center justify-center">
        <span class="block w-full h-0.5 bg-white mb-1.5 transition-all duration-300 transform {isMobileMenuOpen ? 'rotate-45 translate-y-2' : ''}"></span>
        <span class="block w-full h-0.5 bg-white mb-1.5 transition-all duration-300 {isMobileMenuOpen ? 'opacity-0' : 'opacity-100'}"></span>
        <span class="block {isMobileMenuOpen ? 'w-full' : 'w-3/4'} h-0.5 bg-white transition-all duration-300 transform {isMobileMenuOpen ? '-rotate-45 -translate-y-2' : ''} {isMobileMenuOpen ? '' : 'self-end'}"></span>
      </div>
    </button>
  </div>
</header>

<!-- Mobilne menu -->
<div 
  class="md:hidden fixed top-10 left-0 w-full bg-black border-b-2 border-white/20 z-40 transition-all duration-300 overflow-hidden"
  style="max-height: {isMobileMenuOpen ? '400px' : '0'}; opacity: {isMobileMenuOpen ? '1' : '0'}; transform: translateY({isMobileMenuOpen ? '0' : '-10px'});"
  bind:this={menuRef}
>
  <nav class="w-full px-6 py-4">
    <div class="nav-container relative">
      <ul class="flex flex-col space-y-4 text-center" bind:this={mobileNavListRef}>
        <li><a href="#about" class="nav-link text-white text-xl hover:text-accent-silver block py-1" bind:this={mobileNavLinks['about']} onclick={() => closeMobileMenu()}>O Nas</a></li>
        <li><a href="#music" class="nav-link text-white text-xl hover:text-accent-silver block py-1" bind:this={mobileNavLinks['music']} onclick={() => closeMobileMenu()}>Muzyka</a></li>
        <li><a href="#shows" class="nav-link text-white text-xl hover:text-accent-silver block py-1" bind:this={mobileNavLinks['shows']} onclick={() => closeMobileMenu()}>Koncerty</a></li>
        <li><a href="#merch" class="nav-link text-white text-xl hover:text-accent-silver block py-1" bind:this={mobileNavLinks['merch']} onclick={() => closeMobileMenu()}>Merch</a></li>
        <li><a href="#contact" class="nav-link text-white text-xl hover:text-accent-silver block py-1" bind:this={mobileNavLinks['contact']} onclick={() => closeMobileMenu()}>Kontakt</a></li>
      </ul>
      <span class="nav-indicator-mobile" style="top: {mobileIndicatorTop}px; width: {mobileIndicatorWidth}px;"></span>
    </div>
  </nav>
</div>