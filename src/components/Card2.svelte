<script>
  import mpgImage from '../lib/heuristic_histogram_mpg.png';  // Adjust the path to where the image is located
  import insImage from '../lib/ins-Discretization-method-heatmap-1.png';
  import fireImage from '../lib/fire-Discretization-method-heatmap-1.png';
  import bostonImage from '../lib/boston-Discretization-method-heatmap-1.png';

  let currentIndex = 0;

  const cards = [
    {
      title: "Boston Dataset",
      content: `We compare five cases using heat maps: the top two use the Naive method, while the rest correspond to different models and metrics. 
      
      Left-side plots use Meyer’s method, and right-side plots use ZORRO. 
      The figure shows that ZORRO parameters maintain better robustness ratios than Meyer parameters, though the overall error injection effectiveness is slightly worse when comparing ZORRO Leave-One-Out for the same Boston dataset.

      The best error injection method for the Boston dataset appears to be ZORRO Linear Regression Mean Squared Error Cut, which outperforms most ZORRO Leave-One-Out implementations.`,
      image: bostonImage 
    },
    {
      title: "MPG Dataset",
      content: `Fig. 3 shows that ZORRO parameters maintain better robustness ratios than Meyer parameters, though overall error injection effectiveness is similar to Leave One Out with minor differences. 
      Under worst-case scenarios, robustness ratios vary across models and metrics without a clear pattern. 
      For example, ZORRO on Linear Regression with mean absolute error has a similar robustness ratio to Random Forest with mean squared error.
      The best error injection method for the mpg dataset appears to be Linear Regression with mean squared error, showing nearly a 10-percentage-point drop in robustness compared to other model combinations.`,
      image: mpgImage
    },
    {
      title: "Insurance Dataset",
      content: `Fig. 4 shows that ZORRO's robustness ratios are much lower than those from the leave-one-out method in Fig. 2. 
      Except for the 2.6 ratio from linear regression with mean absolute error—just slightly worse than the naive method—all other ratios fall far short.
      Notably, the parameter-metric-model combinations that underperformed the naive method with leave one out (Fig. 2) also did so here.
      Meanwhile, linear regression with mean absolute error, the only combination worse than the naive method in leave one out for insurance data, remains the sole underperformer.
      Overall, the ratio performances have completely flipped between Fig. 2 and Fig. 4.`,
      image: insImage 
    },
    {
      title: "Fire Dataset",
      content: ` `,
      image: fireImage 
    }

  ];

  function scrollToCard(index) {
    currentIndex = index;
    const cardElement = document.getElementById(`card2-carousel-card-${index}`);
    if (cardElement) {
      cardElement.scrollIntoView({ behavior: "smooth", block: "nearest", inline: "center" });
    }
  }
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
</style>

<div class="header-nav">
  {#each cards as card, index}
    <button type="button" on:click={() => scrollToCard(index)}>{card.title}</button>
  {/each}
</div>

<div class="carousel-container">
  <div class="carousel-wrapper" id="carousel-wrapper">
    {#each cards as card, index}
      <div id={`card2-carousel-card-${index}`} class="carousel-card">
        <div class="card">
          <div class="card-header">{card.title}</div>
          <p>{card.content}</p>
          <img src={card.image} alt={card.title} />
        </div>
      </div>
    {/each}
  </div>
</div>
