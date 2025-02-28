<script>
  import mpgImage from '../lib/Multi_Robustness_lineplot_Zorro_Annotated_mpg.png';  // Adjust the path to where the image is located
  import insImage from '../lib/Multi_Robustness_lineplot_Zorro_Annotated_ins.png';
  import fireImage from '../lib/Multi_Robustness_lineplot_Zorro_Annotated_fire.png';
  import bostonImage from '../lib/Multi_Robustness_lineplot_Zorro_Annotated_bos.png';

  let currentIndex = 0;

  const cards = [
    {
      title: "Boston Dataset",
      content: ` `,
      image: bostonImage 
    }

  ];

  function scrollToCard(index) {
    currentIndex = index;
    const cardElement = document.getElementById(`card5-carousel-card-${index}`);
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
    max-width: 60%;
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
  @media (max-width: 768px) {
  .carousel-wrapper {
    width: 95%; /* Make carousel take most of the screen */
    padding: 10px 0;
  }

  .carousel-card {
    min-width: 90%; /* Ensure cards fit within screen */
  }

  .card {
    padding: 20px; /* Reduce padding for smaller screens */
    min-width: 300px; /* Reduce card width */
  }

  .card-header {
    font-size: 1.4em; /* Reduce title size */
    margin-bottom: 10px;
  }

  .card p {
    font-size: 14px; /* Smaller text for readability */
  }

  .card img {
    max-width: 100%; /* Ensure images are fully visible */
  }

  .header-nav {
    flex-wrap: wrap; /* Allow buttons to stack if needed */
    gap: 10px;
  }

  .header-nav button {
    font-size: 14px;
    padding: 8px 15px; /* Reduce padding */
  }
}

@media (max-width: 480px) {
  .carousel-wrapper {
    width: 100%;
    padding: 5px 0;
  }

  .carousel-card {
    min-width: 100%; /* Each card fully occupies the screen */
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
    flex-direction: column; /* Stack buttons vertically */
    gap: 5px;
  }

  .header-nav button {
    width: 90%; /* Full-width buttons */
    font-size: 12px;
  }
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
      <div id={`card5-carousel-card-${index}`} class="carousel-card">
        <div class="card">
          <div class="card-header">{card.title}</div>
          <p>{card.content}</p>
          <img src={card.image} alt={card.title} />
        </div>
      </div>
    {/each}
  </div>
</div>
