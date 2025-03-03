<script>
  import { onMount } from "svelte";
  
  import bostonImage from '../lib/Pattern_Testing_heatmap_BOS.png';
  import mpgImage from '../lib/Pattern_Testing_heatmap_MPG.png';
  import insImage from '../lib/Pattern_testing_heatmap_ins.png';
  import fireImage from '../lib/Pattern_Testing_heatmap_fire.png';

  import bostonPatterns from '../lib/BOS_Patterns.png';
  import mpgPatterns from '../lib/MPG_Patterns.png';
  import insPatterns from '../lib/INS_Patterns.png';
  import firePatterns from '../lib/Fire_Patterns.png';

  let currentIndex = 0;
  let isMobile = false;

  const cards = [
    
    {
      title: "Boston Dataset",
      content: `We compare five cases using heat maps: the top two use the Naive method, while the rest correspond to different models and metrics. 
      Left-side plots use Meyer’s method, and right-side plots use ZORRO. 
      The figure shows that ZORRO parameters maintain better robustness ratios than Meyer parameters.
      Pattern 1 has the best score at 8.8%. This is the lowest score among all patterns. Pattern 1 seems to be better than all Leave-One-Out appraches, and all Heuristic Histogram approaches.`,
      image: bostonImage,

      content2: "Best patterns mined and found",
      image2: bostonPatterns
    },
    {
      title: "MPG Dataset",
      content: `test`,
      image: mpgImage,
      content2: "test",
      image2: mpgPatterns
    },
    {
      title: "Insurance Dataset",
      content: `test`,
      image: insImage,
      content2: "test",
      image2: insPatterns
    },
    {
      title: "Fire Dataset",
      content: `test`,
      image: fireImage,
      content2: "test",
      image2: firePatterns
    }

  ];


    function scrollToCard(index) {
    currentIndex = index;
    const cardElement = document.getElementById(`card3-carousel-card-${index}`);
    if (cardElement) {
      cardElement.scrollIntoView({ behavior: "smooth", block: "nearest", inline: "center" });
    }
  }

  function nextCard() {
    currentIndex = (currentIndex + 1) % cards.length;
    scrollToCard(currentIndex);

    if (event && event.target) {
    const button = event.target;
    
    // Add a short delay before resetting the color
    setTimeout(() => {
      button.style.backgroundColor = "rgb(255, 225, 0)";
      button.style.color = "black";
    }, 100);
  }

  }

  onMount(() => {
    function updateScreenSize() {
      isMobile = window.innerWidth <= 480;
    }

    updateScreenSize();
    window.addEventListener("resize", updateScreenSize);
  });
</script>

<style>
  .carousel-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    width: 100%;
    margin-top: 20px;
    overflow: hidden;
  }

  .carousel-wrapper {
    display: flex;
    overflow-x: auto;
    scroll-behavior: smooth;
    white-space: nowrap;
    width: 80%;
    gap: 10px;
    padding: 20px 0;
  }

  .carousel-card {
    min-width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .card {
    padding: 40px;
    background-color: rgb(255, 225, 0);
    border-radius: 0px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
    min-width: 350px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .card img {
    max-width: 90%;
    height: auto;
    border-radius: 10px;
    margin-bottom: 15px;
  }

  .card p {
    color: black;
    white-space: normal;
    word-wrap: break-word;
    margin: 0;
  }

  .card-header {
    font-size: 1.8em;
    font-weight: bold;
    cursor: pointer;
    color: rgb(0, 0, 0);
    margin-bottom: 20px;
    text-align: center;
  }

  .header-nav {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-bottom: 20px;
  }

  .header-nav button {
    background-color: rgb(255, 225, 0);
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
    color: black;
    border-radius: 5px;
    transition: background-color 0.3s, color 0.3s;
  }

  .header-nav button:hover {
    background-color: black;
    color: rgb(255, 225, 0);
  }

  @media (max-width: 480px) {
    .carousel-wrapper {
      width: 100%;
      padding: 5px 0;
    }

    .carousel-card {
      min-width: 100%;
    }

    .card {
      min-width: 250px;
      padding: 15px;
    }

    .card-header {
      font-size: 1.2em;
    }

    .card p {
      font-size: 12px;
    }

    .header-nav {
      flex-direction: column;
      gap: 5px;
    }

    .header-nav button {
      width: 90%;
      font-size: 12px;
    }
  }
</style>

{#if isMobile}
  <div class="header-nav">
    <button type="button" on:click={nextCard}>Next: {cards[(currentIndex + 1) % cards.length].title}</button>
  </div>
{:else}
  <div class="header-nav">
    {#each cards as card, index}
      <button type="button" on:click={() => scrollToCard(index)}>{card.title}</button>
    {/each}
  </div>
{/if}

<div class="carousel-container">
  <div class="carousel-wrapper" id="carousel-wrapper">
    {#each cards as card, index}
      <div id="card3-carousel-card-{index}" class="carousel-card">
        <div class="card">
          <div class="card-header">{card.title}</div>
          <p>{card.content}</p>
          <img src={card.image} alt={card.title} />
          <p>{card.content2}</p>
          {#if card.image2}
            <img src={card.image2} alt={card.title} />
          {/if}
        </div>
      </div>
    {/each}
  </div>
</div>