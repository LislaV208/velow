<script lang="ts">
  import { onMount } from "svelte";

  let isVisible = $state(false);

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            isVisible = true;
          } else {
            isVisible = false;
          }
        });
      },
      { threshold: 0.1 }
    );

    const section = document.getElementById("merch");
    if (section) observer.observe(section);

    return () => {
      if (section) observer.unobserve(section);
    };
  });
</script>

<section
  id="merch"
  class="section bg-gradient-to-b from-black via-gray-900 to-black py-20 relative"
>
  <div class="absolute inset-0 opacity-10"></div>
  <div
    class="absolute top-0 left-0 w-full h-24 bg-gradient-to-b from-black to-transparent"
  ></div>

  <div class="container mx-auto px-4 relative z-10">
    <div
      class={`transition-all duration-800 delay-50 ${isVisible ? "opacity-100 translate-y-0" : "opacity-0 translate-y-10"}`}
    >
      <h2 class="section-title text-white">Merch</h2>

      <div class="mb-10">
        <p class="text-gray-300 max-w-3xl text-lg">
          Wspieraj zespół kupując nasz oficjalny merch. Wszystkie produkty są
          wysokiej jakości i zaprojektowane z dbałością o detale.
        </p>
      </div>

      <div class="grid sm:grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-8">
        <!-- T-Shirt Tarot -->
        <div
          class="card rounded-lg overflow-hidden bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
          style="transition-delay: 0ms"
        >
          <div
            class="h-70 overflow-hidden relative cursor-pointer flex items-center justify-center"
          >
            <img
              src="/images/merch/image2115.webp"
              alt="T-Shirt Tarot"
              class="w-full h-full object-cover transform hover:scale-105 transition-all duration-500"
            />
          </div>
          <div class="p-5 relative">
            <div class="flex justify-between items-start mb-2">
              <h3
                class="text-xl font-heading text-white group-hover:text-accent-red transition-colors"
              >
                T-Shirt Tarot
              </h3>
              <span
                class="bg-gray-800 px-3 py-1 rounded text-white font-medium group-hover:bg-accent-red/20 transition-colors"
                >70 zł</span
              >
            </div>
            <p class="text-gray-400 text-sm mb-4">Czarny t-shirt z grafiką</p>
            <a
              href="#contact"
              class="btn w-full text-center border-accent-red text-accent-red hover:text-black"
              >Kontakt</a
            >
          </div>
        </div>

        <!-- Bluza z kapturem -->
        <div
          class="card rounded-lg overflow-hidden bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
          style="transition-delay: 100ms"
        >
          <div
            class="h-70 overflow-hidden relative cursor-pointer flex items-center justify-center"
          >
            <img
              src="/images/merch/image00007.webp"
              alt="Bluza z kapturem"
              class="w-full h-full object-cover transform hover:scale-105 transition-all duration-500"
              style="object-position: center 100%;"
            />
          </div>
          <div class="p-5 relative">
            <div class="flex justify-between items-start mb-2">
              <h3
                class="text-xl font-heading text-white group-hover:text-accent-red transition-colors"
              >
                Bluza z kapturem
              </h3>
              <span
                class="bg-gray-800 px-3 py-1 rounded text-white font-medium group-hover:bg-accent-red/20 transition-colors"
                >120 zł</span
              >
            </div>
            <p class="text-gray-400 text-sm mb-4">
              Czarna bluza z logo zespołu na plecach
            </p>
            <a
              href="#contact"
              class="btn w-full text-center border-accent-red text-accent-red hover:text-black"
              >Kontakt</a
            >
          </div>
        </div>

        <!-- Album CD 'Wizje' -->
        <div
          class="card rounded-lg overflow-hidden bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
          style="transition-delay: 200ms"
        >
          <div
            class="h-70 overflow-hidden relative cursor-pointer flex items-center justify-center"
          >
            <img
              src="/images/okladka.webp"
              alt="Album CD 'Wizje'"
              class="w-full h-full object-cover transform hover:scale-105 transition-all duration-500"
            />
          </div>
          <div class="p-5 relative">
            <div class="flex justify-between items-start mb-2">
              <h3
                class="text-xl font-heading text-white group-hover:text-accent-red transition-colors"
              >
                Album CD 'Wizje'
              </h3>
              <span
                class="bg-gray-800 px-3 py-1 rounded text-white font-medium group-hover:bg-accent-red/20 transition-colors"
                >40 zł</span
              >
            </div>
            <p class="text-gray-400 text-sm mb-4">
              Debiutancki album w digipacku z książeczką
            </p>
            <a
              href="#contact"
              class="btn w-full text-center border-accent-red text-accent-red hover:text-black"
              >Kontakt</a
            >
          </div>
        </div>

        <!-- T-Shirt 'Logo' -->
        <div
          class="card rounded-lg overflow-hidden bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
          style="transition-delay: 300ms"
        >
          <div
            class="h-70 overflow-hidden relative cursor-pointer flex items-center justify-center"
          >
            <img
              src="/images/merch/image00001.webp"
              alt="T-Shirt 'Logo'"
              class="w-full h-full object-cover transform hover:scale-105 transition-all duration-500"
              style="object-position: center 70%;"
            />
          </div>
          <div class="p-5 relative">
            <div class="flex justify-between items-start mb-2">
              <h3
                class="text-xl font-heading text-white group-hover:text-accent-red transition-colors"
              >
                T-Shirt 'Logo'
              </h3>
              <span
                class="bg-gray-800 px-3 py-1 rounded text-white font-medium group-hover:bg-accent-red/20 transition-colors"
                >70 zł</span
              >
            </div>
            <p class="text-gray-400 text-sm mb-4">
              Szary t-shirt z nazwą zespołu i logo na plecach
            </p>
            <a
              href="#contact"
              class="btn w-full text-center border-accent-red text-accent-red hover:text-black"
              >Kontakt</a
            >
          </div>
        </div>

        <!-- Torba płócienna -->
        <div
          class="card rounded-lg overflow-hidden bg-black/50 backdrop-blur-sm border border-gray-800 group hover:border-accent-red"
          style="transition-delay: 400ms"
        >
          <div
            class="h-70 overflow-hidden relative cursor-pointer flex items-center justify-center"
          >
            <img
              src="/images/merch/image00005.webp"
              alt="Torba płócienna"
              class="w-full h-full object-cover transform hover:scale-105 transition-all duration-500"
              style="object-position: center 100%;"
            />
          </div>
          <div class="p-5 relative">
            <div class="flex justify-between items-start mb-2">
              <h3
                class="text-xl font-heading text-white group-hover:text-accent-red transition-colors"
              >
                Torba płócienna
              </h3>
              <span
                class="bg-gray-800 px-3 py-1 rounded text-white font-medium group-hover:bg-accent-red/20 transition-colors"
                >30 zł</span
              >
            </div>
            <p class="text-gray-400 text-sm mb-4">
              Czarna torba z nadrukiem logo zespołu
            </p>
            <a
              href="#contact"
              class="btn w-full text-center border-accent-red text-accent-red hover:text-black"
              >Kontakt</a
            >
          </div>
        </div>
      </div>

      <!-- <div class="mt-12 text-center">
        <p class="text-gray-300 mb-6">Masz pytania dotyczące zamówień lub dostępności produktów?</p>
        <div class="relative inline-block group">
          <a href="#contact" class="btn border-accent-red text-accent-red hover:text-black">Kontakt</a>
          <div class="absolute -inset-0.5 bg-accent-red opacity-0 group-hover:opacity-30 blur transition duration-500 rounded-sm"></div>
        </div>
      </div> -->
    </div>
  </div>

  <div
    class="absolute bottom-0 left-0 w-full h-24 bg-gradient-to-t from-black to-transparent"
  ></div>
</section>
