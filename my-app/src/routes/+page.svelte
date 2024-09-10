<script>
  import { onMount } from "svelte";
  onMount(() => {
    const card = document.querySelector(".card");
    card.addEventListener("mousemove", (e) => {
      const cardRect = card.getBoundingClientRect();
      const x = e.clientX - cardRect.left;
      const y = e.clientY - cardRect.top;
      const centerX = cardRect.width / 2;
      const centerY = cardRect.height / 2;
      const rotateX = ((y - centerY) / centerY) * 15;
      const rotateY = ((centerX - x) / centerX) * 15;
      card.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
    });
    card.addEventListener("mouseleave", () => {
      card.style.transform = "rotateX(0) rotateY(0)";
    });
  });
</script>

<body>
  <div class="card-container">
    <div class="card">
      <section class="creditcard-content">
        <h1>Credit Card Details</h1>
      </section>
    </div>
  </div>
</body>

<style>
  body {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .card-container {
    perspective: 1000px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .card {
    position: relative;
    width: 850px;
    height: 500px;
    background: black;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    transition:
      transform 0.3 easy-in-out,
      box-shadow 0.3 ease-in-out;
    transform-style: preserve-3d;
    cursor: pointer;
  }
  .creditcard-content {
    display: flex;
    width: 850px;
    height: 500px;
    color: white;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
</style>
