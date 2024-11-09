<script lang="ts">
  import { onMount } from 'svelte';
  import { Menu, X, ChevronRight, ChevronLeft } from 'lucide-svelte';
  import desktopImgage1 from '$lib/assets/desktop-image-hero-1.jpg?enhanced';
  import desktopImgage2 from '$lib/assets/desktop-image-hero-2.jpg?enhanced';
  import desktopImgage3 from '$lib/assets/desktop-image-hero-3.jpg?enhanced';
  import darkImage from '$lib/assets/image-about-dark.jpg?enhanced';
  import lightImage from '$lib/assets/image-about-light.jpg?enhanced';
  
  const slides = [
    {
      src: desktopImgage1,
      title: 'Discover innovative ways to decorate',
      description: 'We provide unmatched quality, comfort, and style for property owners across the country. Our experts combine form and function in bringing your vision to life. Create a room in your own style with our collection and make your property a reflection of you and what you love.'
    },
    {
      src: desktopImgage2,
      title: 'We are available all across the globe',
      description: 'With stores all over the world, it\'s easy for you to find furniture for your home or place of business. Locally, we\'re in most major cities throughout the country. Find the branch nearest you using our store locator. Any questions? Don\'t hesitate to contact us today.'
    },
    {
      src: desktopImgage3,
      title: 'Manufactured with the best materials',
      description: 'Our modern furniture store provide a high level of quality. Our company has invested in advanced technology to ensure that every product is made as perfect and as consistent as possible. With three decades of experience in this industry, we understand what customers want for their home and office.'
    }
  ];

  let currentSlide = 0;
  let isMenuOpen = false;

  function nextSlide() {
    currentSlide = (currentSlide + 1) % slides.length;
  }

  function prevSlide() {
    currentSlide = (currentSlide - 1 + slides.length) % slides.length;
  }

  onMount(() => {
    const handleKeydown = (e: KeyboardEvent) => {
      if (e.key === 'ArrowLeft') prevSlide();
      if (e.key === 'ArrowRight') nextSlide();
    };

    window.addEventListener('keydown', handleKeydown);
    return () => window.removeEventListener('keydown', handleKeydown);
  });
</script>

<div class="relative">
  <!-- Navigation -->
  <nav class="absolute w-full z-40 px-8 md:px-16 py-12 flex items-center">
    <div class="flex items-center">
      <button 
        class="md:hidden mr-6 text-white"
        on:click={() => isMenuOpen = !isMenuOpen}
        aria-label="Toggle menu"
      >
        <Menu class="w-6 h-6" />
      </button>
      <a href="/" class="text-2xl font-bold tracking-wide text-white">room</a>
    </div>
    
    <!-- Desktop Navigation -->
    <div class="hidden md:flex items-center space-x-8 text-white ml-12">
      <a href="#" class="hover:underline">home</a>
      <a href="#" class="hover:underline">shop</a>
      <a href="#" class="hover:underline">about</a>
      <a href="#" class="hover:underline">contact</a>
    </div>
  </nav>

  <!-- Mobile Menu -->
  {#if isMenuOpen}
    <div class="fixed inset-0 bg-white h-24 z-50 md:hidden">
      <div class="flex justify-between items-center px-8 py-12">
        <button 
          class="text-black"
          on:click={() => isMenuOpen = false}
          aria-label="Close menu"
        >
          <X class="w-6 h-6" />
        </button>
        <div class="flex space-x-8">
          <a href="#" class="text-black hover:underline">home</a>
          <a href="#" class="text-black hover:underline">shop</a>
          <a href="#" class="text-black hover:underline">about</a>
          <a href="#" class="text-black hover:underline">contact</a>
        </div>
      </div>
    </div>
  {/if}

  <!-- Main Content -->
  <div class="flex flex-col lg:flex-row">
    <!-- Image Section -->
    <div class="relative w-full lg:w-[60%]">
      <enhanced:img
        src={slides[currentSlide].src}
        alt="Furniture showcase"
        class="w-full h-[360px] lg:h-full object-cover"
      />
      
      <!-- Slider Controls -->
      <div class="absolute bottom-0 right-0 lg:translate-x-full flex">
        <button
          class="p-6 bg-black hover:bg-gray-800 transition-colors focus:outline-none"
          on:click={prevSlide}
          aria-label="Previous slide"
        >
          <ChevronLeft class="w-6 h-6 text-white" />
        </button>
        <button
          class="p-6 bg-black hover:bg-gray-800 transition-colors focus:outline-none"
          on:click={nextSlide}
          aria-label="Next slide"
        >
          <ChevronRight class="w-6 h-6 text-white" />
        </button>
      </div>
    </div>

    <!-- Content Section -->
    <div class="w-full lg:w-[40%] p-8 md:p-20 lg:p-24 flex flex-col justify-center">
      <h1 class="text-4xl lg:text-5xl font-bold mb-6 leading-tight">
        {slides[currentSlide].title}
      </h1>
      <p class="text-gray-500 mb-8">
        {slides[currentSlide].description}
      </p>
      <a 
        href="#"
        class="inline-flex items-center text-sm tracking-[0.8em] uppercase hover:text-gray-500 transition-colors group"
      >
        Shop now
        <ChevronRight class="w-8 h-8 ml-4 group-hover:translate-x-1 transition-transform" />
      </a>
    </div>
  </div>

  <!-- About Section -->
  <div class="grid lg:grid-cols-3">
    <div class="md:h-96">
      <enhanced:img src={lightImage} alt="Furniture detail" class="w-full h-full object-cover" /> 
    </div>
    <div class="p-8 md:h-96 lg:p-16 flex flex-col justify-center md:gap-5 lg:gap-0">
      <h2 class="text-sm uppercase tracking-[0.5em] font-bold mb-4">
        About our furniture
      </h2>
      <p class="text-gray-500">
        Our multifunctional collection blends design and function to suit your individual taste. Make each room unique, or pick a cohesive theme that best express your interests and what inspires you. Find the furniture pieces you need, from traditional to contemporary styles or anything in between. Product specialists are available to help you create your dream space.
      </p>
    </div>
    <div class="md:h-96">
      <enhanced:img src={darkImage} alt="Furniture detail" class="w-full h-full object-cover" />
    </div>
  </div>
</div>

<style>
  :global(body) {
    @apply overflow-x-hidden;
  }
</style>