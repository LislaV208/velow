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
    
    const section = document.getElementById('contact');
    if (section) observer.observe(section);
    
    return () => {
      if (section) observer.unobserve(section);
    };
  });
  
  let name = '';
  let email = '';
  let message = '';
  let submitted = false;
  
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
</script>

<section id="contact" class="section bg-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <div class={`transition-all duration-1000 delay-300 ${isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="section-title text-white">Kontakt</h2>
      
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
        <div>
          <h3 class="text-3xl font-heading text-white mb-6 relative inline-block distortion-border pb-3">Napisz do nas</h3>
          
          {#if submitted}
            <div class="bg-accent-red/20 border border-accent-red text-white p-4 rounded-lg mb-6 animate-fade-in">
              <div class="flex items-center">
                <svg class="w-5 h-5 mr-2 text-accent-red" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                </svg>
                <span>Dziękujemy za wiadomość! Odpowiemy najszybciej jak to możliwe.</span>
              </div>
            </div>
          {/if}
          
          <form on:submit|preventDefault={handleSubmit} class="space-y-6">
            <div>
              <label for="name" class="block text-white mb-2">Imię i nazwisko</label>
              <input 
                type="text" 
                id="name" 
                bind:value={name} 
                required
                class="w-full bg-gray-800/50 backdrop-blur-sm border border-gray-700 rounded-lg px-4 py-3 text-white focus:outline-none focus:ring-2 focus:ring-accent-red focus:border-transparent"
              >
            </div>
            
            <div>
              <label for="email" class="block text-white mb-2">Email</label>
              <input 
                type="email" 
                id="email" 
                bind:value={email} 
                required
                class="w-full bg-gray-800/50 backdrop-blur-sm border border-gray-700 rounded-lg px-4 py-3 text-white focus:outline-none focus:ring-2 focus:ring-accent-red focus:border-transparent"
              >
            </div>
            
            <div>
              <label for="message" class="block text-white mb-2">Wiadomość</label>
              <textarea 
                id="message" 
                bind:value={message} 
                required
                rows="5"
                class="w-full bg-gray-800/50 backdrop-blur-sm border border-gray-700 rounded-lg px-4 py-3 text-white focus:outline-none focus:ring-2 focus:ring-accent-red focus:border-transparent"
              ></textarea>
            </div>
            
            <div class="relative inline-block group">
              <button type="submit" class="btn border-accent-red text-accent-red hover:text-black">Wyślij wiadomość</button>
              <div class="absolute -inset-0.5 bg-accent-red opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
            </div>
          </form>
        </div>
        
        <div>
          <h3 class="text-3xl font-heading text-white mb-6 relative inline-block distortion-border pb-3">Informacje kontaktowe</h3>
          
          <div class="space-y-8">
            <div class="bg-gray-900/30 backdrop-blur-sm p-6 rounded-lg border border-gray-800 hover:border-accent-red transition-colors duration-300">
              <h4 class="text-xl font-heading text-accent-red mb-2">Ogólny kontakt</h4>
              <p class="text-gray-300">Email: <a href="mailto:kontakt@velow.pl" class="text-white hover:text-accent-red transition-colors">kontakt@velow.pl</a></p>
              <p class="text-gray-300">Telefon: <a href="tel:+48123456789" class="text-white hover:text-accent-red transition-colors">+48 123 456 789</a></p>
            </div>
            
            <div class="bg-gray-900/30 backdrop-blur-sm p-6 rounded-lg border border-gray-800 hover:border-accent-red transition-colors duration-300">
              <h4 class="text-xl font-heading text-accent-red mb-2">Booking koncertów</h4>
              <p class="text-gray-300">Email: <a href="mailto:koncerty@velow.pl" class="text-white hover:text-accent-red transition-colors">koncerty@velow.pl</a></p>
              <p class="text-gray-300">Telefon: <a href="tel:+48987654321" class="text-white hover:text-accent-red transition-colors">+48 987 654 321</a></p>
            </div>
            
            <div class="bg-gray-900/30 backdrop-blur-sm p-6 rounded-lg border border-gray-800 hover:border-accent-red transition-colors duration-300">
              <h4 class="text-xl font-heading text-accent-red mb-2">Management</h4>
              <p class="text-gray-300">Nazwa: Rock Management</p>
              <p class="text-gray-300">Email: <a href="mailto:manager@velow.pl" class="text-white hover:text-accent-red transition-colors">manager@velow.pl</a></p>
            </div>
            
            <div class="bg-gray-900/30 backdrop-blur-sm p-6 rounded-lg border border-gray-800 hover:border-accent-red transition-colors duration-300">
              <h4 class="text-xl font-heading text-accent-red mb-2">Media społecznościowe</h4>
              <div class="flex space-x-4 mt-3">
                <a href="https://facebook.com" target="_blank" rel="noopener noreferrer" class="text-gray-400 hover:text-accent-red transition-colors">
                  <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
                  </svg>
                </a>
                <a href="https://instagram.com" target="_blank" rel="noopener noreferrer" class="text-gray-400 hover:text-accent-red transition-colors">
                  <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd" />
                  </svg>
                </a>
                <a href="https://youtube.com" target="_blank" rel="noopener noreferrer" class="text-gray-400 hover:text-accent-red transition-colors">
                  <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path fill-rule="evenodd" d="M19.812 5.418c.861.23 1.538.907 1.768 1.768C21.998 8.746 22 12 22 12s0 3.255-.418 4.814a2.504 2.504 0 0 1-1.768 1.768c-1.56.419-7.814.419-7.814.419s-6.255 0-7.814-.419a2.505 2.505 0 0 1-1.768-1.768C2 15.255 2 12 2 12s0-3.255.417-4.814a2.507 2.507 0 0 1 1.768-1.768C5.744 5 11.998 5 11.998 5s6.255 0 7.814.418ZM15.194 12 10 15V9l5.194 3Z" clip-rule="evenodd" />
                  </svg>
                </a>
                <a href="https://spotify.com" target="_blank" rel="noopener noreferrer" class="text-gray-400 hover:text-accent-red transition-colors">
                  <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/>
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>