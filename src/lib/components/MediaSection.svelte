<script lang="ts">
  import { onMount } from 'svelte';
  
  const photos = [
    { src: "/images/gallery1.jpg", alt: "Koncert w Warszawie" },
    { src: "/images/gallery2.jpg", alt: "Backstage" },
    { src: "/images/gallery3.jpg", alt: "Sesja zdjęciowa" },
    { src: "/images/gallery4.jpg", alt: "Festiwal rockowy" },
    { src: "/images/gallery5.jpg", alt: "W studiu" },
    { src: "/images/gallery6.jpg", alt: "Próba zespołu" }
  ];
  
  const videos = [
    { 
      title: "Pierwszy Krok - Official Video",
      embedUrl: "https://www.youtube.com/embed/placeholder1",
      thumbnail: "/images/video-thumb1.jpg"
    },
    { 
      title: "Ciemna Strona - Live",
      embedUrl: "https://www.youtube.com/embed/placeholder2",
      thumbnail: "/images/video-thumb2.jpg"
    },
    { 
      title: "Wywiad z zespołem",
      embedUrl: "https://www.youtube.com/embed/placeholder3",
      thumbnail: "/images/video-thumb3.jpg"
    }
  ];
  
  let selectedVideo = $state(videos[0]);
  let isGalleryVisible = $state(false);
  let isVideoVisible = $state(false);
  
  function selectVideo(video) {
    selectedVideo = video;
  }
  
  onMount(() => {
    const videoObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isVideoVisible = true;
        }
      });
    }, { threshold: 0.1 });
    
    const galleryObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          isGalleryVisible = true;
        }
      });
    }, { threshold: 0.1 });
    
    const videoSection = document.querySelector('.video-section');
    const gallery = document.querySelector('.gallery-grid');
    
    if (videoSection) videoObserver.observe(videoSection);
    if (gallery) galleryObserver.observe(gallery);
    
    return () => {
      if (videoSection) videoObserver.unobserve(videoSection);
      if (gallery) galleryObserver.unobserve(gallery);
    };
  });
</script>

<section id="media" class="section bg-black py-20 relative">
  <div class="absolute inset-0 bg-noise-pattern opacity-10"></div>
  <div class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"></div>
  
  <div class="container mx-auto px-4 relative z-10">
    <h2 class="section-title text-white">Media</h2>
    
    <div class="mb-16 video-section">
      <div class={`transition-all duration-1000 delay-300 ${isVideoVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
        <h3 class="text-3xl font-heading text-white mb-8 relative inline-block distortion-border pb-3">Wideo</h3>
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
          <div class="lg:col-span-2">
            <div class="bg-gray-900/50 backdrop-blur-sm rounded-lg overflow-hidden border border-gray-800 group relative">
              <div class="absolute -inset-0.5 bg-gradient-to-r from-accent-red to-transparent opacity-0 group-hover:opacity-20 blur-sm transition-opacity duration-700"></div>
              <div class="aspect-video relative z-10">
                <iframe width="100%" height="100%" src={selectedVideo.embedUrl} title={selectedVideo.title} frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
              </div>
              <div class="p-4 relative z-10">
                <h4 class="text-white font-medium text-lg">{selectedVideo.title}</h4>
              </div>
            </div>
          </div>
          
          <div class="space-y-4">
            {#each videos as video, i}
              <div 
                class={`p-2 rounded-lg cursor-pointer transition-all duration-300 ${selectedVideo === video ? 'bg-accent-red/20 border-l-4 border-accent-red' : 'bg-gray-900/50 hover:bg-gray-800/50'}`}
                onclick={() => selectVideo(video)}
                onkeydown={(e) => e.key === 'Enter' && selectVideo(video)}
                tabindex="0"
                role="button"
                style="transition-delay: {i * 100}ms"
              >
                <div class="flex space-x-3">
                  <div class="w-24 h-16 flex-shrink-0 overflow-hidden rounded">
                    <img src={video.thumbnail} alt={video.title} class="w-full h-full object-cover transition-transform duration-500 hover:scale-110">
                  </div>
                  <div class="flex-grow">
                    <h5 class="text-white text-sm font-medium">{video.title}</h5>
                  </div>
                </div>
              </div>
            {/each}
            
            <a href="https://www.youtube.com/channel/" target="_blank" rel="noopener noreferrer" class="btn w-full text-center border-accent-red text-accent-red hover:text-black">
              <span class="flex items-center justify-center">
                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/>
                </svg>
                Zobacz więcej na YouTube
              </span>
            </a>
          </div>
        </div>
      </div>
    </div>
    
    <div>
      <h3 class="text-3xl font-heading text-white mb-8 relative inline-block distortion-border pb-3">Galeria</h3>
      
      <div class={`gallery-grid grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 transition-all duration-1000 ${isGalleryVisible ? 'opacity-100' : 'opacity-0'}`}>
        {#each photos as photo, i}
          <div 
            class="overflow-hidden rounded-lg aspect-square group relative"
            style={`transition-delay: ${i * 100}ms`}
          >
            <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 z-10"></div>
            <img 
              src={photo.src} 
              alt={photo.alt} 
              class="w-full h-full object-cover grayscale hover:grayscale-0 transition-all duration-500 transform group-hover:scale-105"
            >
            <div class="absolute bottom-0 left-0 p-4 transform translate-y-full group-hover:translate-y-0 transition-transform duration-300 z-20">
              <p class="text-white font-medium">{photo.alt}</p>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
  
  <div class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"></div>
</section>