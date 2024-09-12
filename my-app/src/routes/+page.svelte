<script>
  import { onMount } from "svelte";

  onMount(() => {
    const card = document.querySelector(".card");

    document.addEventListener("mousemove", (e) => {
      const cardRect = card.getBoundingClientRect();
      const x = e.clientX - cardRect.left;
      const y = e.clientY - cardRect.top;
      const centerX = cardRect.width / 2;
      const centerY = cardRect.height / 2;

      const screenWidth = window.innerWidth;
      const screenHeight = window.innerHeight;
      const activeWidth = screenWidth * 0.9;
      const activeHeight = screenHeight * 0.9;
      const offsetX = (screenWidth - activeWidth) / 2;
      const offsetY = (screenHeight - activeHeight) / 2;

      let rotateX = 0;
      let rotateY = 0;

      if (
        e.clientX > offsetX &&
        e.clientX < offsetX + activeWidth &&
        e.clientY > offsetY &&
        e.clientY < offsetY + activeHeight
      ) {
        rotateX = ((y - centerY) / centerY) * 15;
        rotateY = ((centerX - x) / centerX) * 15;
      }

      card.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
      card.style.setProperty("--mouse-x", `${x}px`);
      card.style.setProperty("--mouse-y", `${y}px`);
    });
  });
</script>

<body>
  <div class="card-container">
    <div class="card">
      <div class="holographic-bg"></div>
      <section class="creditcard-content">
        <h1>Credit Card</h1>
        <article class="Name-details">
          <h2>Name Cardholder</h2>
          <p>Ilona van Oosbree</p>
        </article>
      </section>
    </div>
  </div>
</body>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Fira+Sans:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

  body {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #f0f0f0;
  }
  .card-container {
    perspective: 1000px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .card {
    position: relative;
    width: clamp(300px, 50vw, 850px);
    height: clamp(200px, 30vw, 500px);
    background: rgba(136, 0, 255, 0.3);
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    transition:
      box-shadow 0.3s ease-in-out,
      background 0.3s ease-in-out,
      transform 0.1s ease-out,
      width 0.3s ease-in-out,
      height 0.3s ease-in-out;
    transform-style: preserve-3d;
    cursor: pointer;
    --mouse-x: 50%;
    --mouse-y: 50%;
    background-image: linear-gradient(
      45deg,
      rgba(255, 255, 255, 0.05) 25%,
      transparent 25%,
      transparent 50%,
      rgba(255, 255, 255, 0.162) 50%,
      rgba(255, 255, 255, 0.05) 75%,
      transparent 75%,
      transparent
    );
    background-size: 50px 50px;
  }
  .card:hover {
    background-image: linear-gradient(
      45deg,
      rgba(255, 255, 255, 0.716) 25%,
      transparent 25%,
      transparent 50%,
      rgb(255, 255, 255) 50%,
      rgba(255, 255, 255, 0) 75%,
      transparent 75%,
      transparent
    );
  }
  .holographic-bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(
      circle at var(--mouse-x) var(--mouse-y),
      rgba(255, 255, 255, 0.5),
      rgba(0, 0, 255, 0.2),
      rgba(0, 0, 0, 0.3),
      rgba(0, 0, 255, 0.3)
    );
    background-size: 200% 200%;
    transition:
      background-position 0.3s ease-in-out,
      opacity 0.3s ease-in-out;
    pointer-events: none;
    opacity: 0;
    z-index: 0;
  }
  .card:hover .holographic-bg {
    opacity: 1;
  }
  .creditcard-content {
    font-family: "Fira Sans", sans-serif;
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: black;
    z-index: 1;
    text-align: center;
    padding: 1rem;
  }

  .creditcard-content h1 {
    font-size: clamp(1.5rem, 2.5vw, 3rem);
    margin: 0.5rem 0;
  }

  .creditcard-content h2 {
    font-size: clamp(1.25rem, 2vw, 2.5rem);
    margin: 0.5rem 0;
  }

  .creditcard-content p {
    font-size: clamp(1rem, 1.5vw, 2rem);
    margin: 0.5rem 0;
  }

  .creditcard-content h1,
  .creditcard-content h2,
  .creditcard-content p {
    text-shadow: 2px 2px 5px rgba(245, 210, 255, 0.983); /* Added text shadow */
  }
</style>
