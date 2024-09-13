<script>
  import logo from "../assets/soapsleeve.jpg";
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
  <article class="card-container">
    <article class="card">
      <div class="holographic-bg"></div>
      <section class="creditcard-content">
        <h1>Credit Card</h1>
        <article class="cardnumber">
          <p>123 456 7890</p>
        </article>
        <div class="details-spacearound">
          <article class="name-details">
            <h2>Cardholder</h2>
            <p>Ilona van Oosbree</p>
          </article>
          <article class="expiration-date">
            <h2>Expires</h2>
            <p>06/25</p>
          </article>
        </div>
      </section>
    </article>
  </article>
</body>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Orbitron:wght@400..900&display=swap");
  body {
    font-family: "Orbitron", sans-serif;
    letter-spacing: 2px;
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
    height: clamp(200px, 30vw, 500px);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin: 0 0 0 4rem;
  }

  .creditcard-content h1 {
    z-index: 2;
    font-weight: 500;
    font-size: 1.5rem;
    text-transform: uppercase;
    color: black;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  }

  .creditcard-content .cardnumber {
    z-index: 2;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2.5rem;
    letter-spacing: 1rem;
    color: black;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  }

  .details-spacearound {
    display: flex;
    justify-content: space-between;
  }

  .creditcard-content .name-details,
  .creditcard-content .expiration-date {
    z-index: 2;
    color: black;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
    margin: 0 5rem 1rem 0;
    & h2 {
      font-size: 0.7rem;
      font-weight: 500;
    }

    & p {
      font-size: 1.5rem;
      font-weight: 300;
    }
  }
</style>
