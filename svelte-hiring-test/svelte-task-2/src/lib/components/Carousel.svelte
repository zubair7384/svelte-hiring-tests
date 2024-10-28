<script lang="ts">
  import { onMount } from "svelte";
    import { writable } from "svelte/store";
  
      interface CarouselItem {
          id: string;
          src: string;
          alt: string;
      }
  
      export let items: CarouselItem[] = [];
  
      let currentIndex = writable(0)
  
      function handleNextSlide() {
          currentIndex.update((i)=>(i + 1 % items.length))
      }

      function handlePrevSlide() {
        currentIndex.update((i)=>(i - 1 + items.length % items.length))
      }

      function onSlideClick(index: number) {
        currentIndex.set(index)
      }

      onMount(()=> {
        const slideInterval = setInterval(handleNextSlide, 2000);
        return () => clearInterval(slideInterval)
      })

  </script>
  
  <div class="carousel">
      <!-- Carousel structure goes here -->
       <div class="carousel__container">
          <div class="carousel__track"
          style="transform: translateX({$currentIndex * -100}%)"
          >
              {#each items as item (item.id)}
                  <div class="carousel__slide">
                      <img class="carousel__image" src={item.src} alt={item.alt} />
                  </div>
              {/each}
          </div>
          <button
          class="carousel__arrow carousel__arrow--left"
          on:click={handlePrevSlide}
          aria-label= "Previous slide">&#8249</button>
          <button
          class="carousel__arrow carousel__arrow--right"
          on:click={handleNextSlide}
          aria-label= "Previous slide">&#8250</button>
       </div>
       <div class="carousel__dots">
        {#each items as _, index}
        <buttons
        class="carousel__dot {index === $currentIndex ? "carousel__dot--active":''}"
        on:click={()=> onSlideClick(index)}
        ></buttons>
        {/each}
       </div>
  </div>
  
  <style>
      .carousel {
          width: 100%;
          max-width: 800px;
          margin: 0 auto;
          position: relative;
      }
  
      .carousel__container {
          position: relative;
          overflow: hidden;
          aspect-ratio: 16/9;
      }
  
      .carousel__track {
          display: flex;
          width: 100%;
          transition: transform 0.3s ease-in-out;
      }
  
      .carousel__slide {
          flex: 0 0 100%;
          width: 100%;
      }
  
      .carousel__image {
          width: 100%;
          height: 100%;
          object-fit: cover;
      }
  
      .carousel__arrow {
          position: absolute;
          top: 50%;
          transform: translateY(-50%);
          background: rgba(255, 255, 255, 0.7);
          border: none;
          border-radius: 50%;
          width: 40px;
          height: 40px;
          cursor: pointer;
          font-size: 20px;
          display: flex;
          align-items: center;
          justify-content: center;
          transition: background-color 0.3s;
          z-index: 1;
      }
  
      .carousel__arrow:hover {
          background: rgba(255, 255, 255, 0.9);
      }
  
      .carousel__arrow--left {
          left: 10px;
      }
  
      .carousel__arrow--right {
          right: 10px;
      }
  
      .carousel__dots {
          position: absolute;
          bottom: 15px;
          left: 50%;
          transform: translateX(-50%);
          display: flex;
          gap: 8px;
          padding: 5px 10px;
          background: rgba(0, 0, 0, 0.2);
          border-radius: 20px;
          z-index: 1;
      }
  
      .carousel__dot {
          width: 10px;
          height: 10px;
          border-radius: 50%;
          border: none;
          background: rgba(255, 255, 255, 0.5);
          cursor: pointer;
          padding: 0;
          transition: background-color 0.3s;
      }
  
      .carousel__dot--active {
          background: white;
      }
  
      @media (max-width: 768px) {
          .carousel__arrow {
              width: 32px;
              height: 32px;
              font-size: 16px;
          }
      }
  </style>
  