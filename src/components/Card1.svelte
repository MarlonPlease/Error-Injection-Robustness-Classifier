<script>
  import { onMount } from "svelte";

  import mpgImage from '../lib/mpg_leave_one_out-1.jpg';  // Adjust the path to where the image is located
  import insImage from '../lib/ins_leave_one_out-1.jpg';
  import fireImage from '../lib/fire_leave_one_out-1.jpg';
  import bostonImage from '../lib/boston_leave_one_out-1.jpg';

  let currentIndex = 0;
  let isMobile = false;

  const cards = [
    {
      title: "Boston Dataset",
      content: `The figure shows robustness ratios deteriorating as uncertainty increases. 
      We compare five cases using heat maps: the top two use the Naive method, 
      while the rest correspond to different models and metrics. 
      Left-side plots use Meyer’s method, and right-side plots use ZORRO. 
      ZORRO demonstrates superior robustness in handling uncertain data compared to Meyer et al.’s method across all tested conditions.
      The ZORRO methods staying above 11% even under extreme uncertainty, 
      while Meyer drops to near zero. 
      Among methods, ZORRO Leave-one-out(LOO) with Random Forest and mean absolute error delivers the strongest attack on robustness with 11.8%.
      All other ZORRO methods show similar scores, while ZORRO Leave-one-out(LOO) with Random Forest and mean squared error was the worst performing.
       `,
      image: bostonImage // Replace with an actual image file in public/images/
    },
    {
      title: "MPG Dataset",
      content: `Fig. 1 shows robustness ratios deteriorating as uncertainty increases. 
      We compare five cases using heat maps: the top two use the Naive method, while the rest correspond to different models and metrics. Left-side plots use Meyer’s method, and right-side plots use ZORRO. 
      ZORRO retains robustness better, staying above 50% even under extreme uncertainty, while Meyer drops to near zero. Among methods, Linear Regression with mean absolute error delivers the strongest attack on robustness, outperforming RandomForestRegressor.`,
      image: mpgImage
    },
    {
      title: "Insurance Dataset",
      content: `In Fig 2. , we see the results of different types of robustness test error injections against the
      naive randomization method`,
      image: insImage // Replace with an actual image file in public/images/
    },
    {
      title: "Fire Dataset",
      content: ` `,
      image: fireImage // Replace with an actual image file in public/images/
    }
    
  ];

    function scrollToCard(index) {
    currentIndex = index;
    const cardElement = document.getElementById(`card-carousel-card-${index}`);
    if (cardElement) {
      cardElement.scrollIntoView({ behavior: "smooth", block: "nearest", inline: "center" });
    }
  }

  function nextCard() {
    currentIndex = (currentIndex + 1) % cards.length;
    scrollToCard(currentIndex);

    if (event && event.target) {
    setTimeout(() => {
      event.target.blur();
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
      <div id="card-carousel-card-{index}" class="carousel-card">
        <div class="card">
          <div class="card-header">{card.title}</div>
          <p>{card.content}</p>
          <img src={card.image} alt={card.title} />
          
          
        </div>
      </div>
    {/each}
  </div>
</div>