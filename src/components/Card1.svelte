<script>
  let currentIndex = 0;

  const cards = [
    { title: "Card 1", content: "This is the first card." },
    { title: "Card 2", content: "This is the second card." },
    { title: "Card 3", content: "This is the third card." }
  ];

  function scrollToCard(index) {
    currentIndex = index; // Update the current card index
    const cardElement = document.getElementById(`carousel-card-${index}`);
    cardElement.scrollIntoView({ behavior: 'smooth', block: 'center' });
  }
</script>

<style>
  .carousel-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    width: 100%;
    height: auto;
    overflow-y: auto;
    margin-top: 20px;
  }

  .carousel {
    display: flex;
    width: 80vw;
    height: 60vh;
    background-color: rgb(255, 225, 0);
    border-radius: 10px;
    padding: 20px;
    text-align: center;
    position: relative;
    overflow: hidden;
    justify-content: center;
    flex-direction: column;
  }

  .card {
    padding: 40px; /* Increased padding for larger cards */
    background-color: rgb(255, 225, 0);
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
    min-width: 350px; /* Increased card size */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .card-header {
    font-size: 1.8em; /* Larger font size for the title */
    font-weight: bold;
    cursor: pointer;
    color: rgb(0, 0, 0);
    margin-bottom: 20px; /* Space between title and content */
    text-align: center; /* Center the title */
  }

  .card-header:hover {
    color: rgb(255, 225, 0);
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
    color: white;
    border-radius: 5px;
    transition: background-color 0.3s;
  }

  .header-nav button:hover {
    background-color: rgb(255, 255, 255);
    color: rgb(0, 0, 0);
  }

  .card-container {
    display: flex;
    gap: 10px;
    width: 100%;
    overflow-x: auto;
  }

  .carousel-card {
    min-width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .carousel-wrapper {
    display: flex;
    overflow-x: auto;
    transition: transform 0.3s ease;
  }
</style>

<!-- Card Navigation Header -->
<div class="header-nav">
  {#each cards as card, index}
    <button on:click={() => scrollToCard(index)}>{card.title}</button>
  {/each}
</div>

<!-- Carousel -->
<div class="carousel-container">
  <div class="carousel-wrapper" id="carousel-wrapper">
    <!-- Cards inside the carousel -->
    {#each cards as card, index}
      <div id="carousel-card-{index}" class="carousel-card">
        <div class="card">
          <div class="card-header">{card.title}</div>
          <p>{card.content}</p>
        </div>
      </div>
    {/each}
  </div>
</div>
