<script>
  export let images = [];
  export let interval = 5000; // Thời gian chuyển ảnh (ms)
  
  let currentIndex = 0;
  
  // Tự động chuyển ảnh mỗi 5 giây
  import { onMount, onDestroy } from 'svelte';
  
  let timer;
  
  function startAutoSlide() {
    timer = setInterval(() => {
      currentIndex = (currentIndex + 1) % images.length;
    }, interval);
  }
  
  onMount(() => {
    if (images.length > 1) {
      startAutoSlide();
    }
  });
  
  onDestroy(() => {
    if (timer) clearInterval(timer);
  });
</script>

<div class="slider-container">
  {#each images as image, i}
    <div class="slide" class:active={i === currentIndex}>
      <img src={image} alt="TMAI Saigon" />
    </div>
  {/each}
  
  <!-- Indicators -->
  <div class="slider-dots">
    {#each images as _, i}
      <span 
        class="dot" 
        class:active={i === currentIndex}
        on:click={() => currentIndex = i}
      ></span>
    {/each}
  </div>
</div>

<style>
  .slider-container {
    width: 100%;
    height: 100vh; /* Full viewport height */
    overflow: hidden;
    position: relative;
  }
  
  .slide {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
    transition: opacity 1.5s ease-in-out;
    z-index: 1;
  }
  
  .slide.active {
    opacity: 1;
    z-index: 2;
  }
  
  .slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  .slider-dots {
    position: absolute;
    bottom: 40px; /* Đẩy chấm xuống gần phía dưới viewport */
    width: 100%;
    display: none;
    justify-content: center;
    z-index: 3;
  }
  
  .dot {
    cursor: pointer;
    height: 12px;
    width: 12px;
    margin: 0 5px;
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 50%;
    display: inline-block;
    transition: background-color 0.3s;
  }
  
  .dot:hover, .dot.active {
    background-color: #ffffff;
  }
</style>