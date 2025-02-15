<script>
  
  
  import boston_normalized from '../lib/boston_normalized.png';
  import boston_compared from '../lib/boston_compared.png';

  let currentIndex = 0;

  const cards = [
  {
    title: "Boston Dataset",
    content: "Method comparisons across the Boston Dataset",
    image: boston_normalized,
    content2: "Comparing the Robustness of “Boston” to other datasets",
    image2: boston_compared
  }
];

  function scrollToCard(index) {
    currentIndex = index;
    const cardElement = document.getElementById(`card4-carousel-card-${index}`);
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
      <div id={`card4-carousel-card-${index}`} class="carousel-card">
        <div class="card">
          <div class="card-header">{card.title}</div>
          <p>{card.content}</p>
          <img src={card.image} alt={card.title} />
          <p>{card.content2}</p>
          <img src={card.image2} alt={card.title} />
        </div>
      </div>
    {/each}
  </div>
</div>
