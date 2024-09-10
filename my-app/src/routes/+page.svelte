<script>
  import { onMount } from "svelte";
  onMount(() => {
    const card = document.querySelector(".card");
    const screenWidth = window.innerWidth;
    const screenHeight = window.innerHeight;
    const activeWidth = screenWidth * 0.8;
    const activeHeight = screenHeight * 0.8;
    const offsetX = (screenWidth - activeWidth) / 2;
    const offsetY = (screenHeight - activeHeight) / 2;
    const boundary = 50; // Distance from the boundary to start smoothing

    document.addEventListener("mousemove", (e) => {
      const cardRect = card.getBoundingClientRect();
      const x = e.clientX - cardRect.left;
      const y = e.clientY - cardRect.top;
      const centerX = cardRect.width / 2;
      const centerY = cardRect.height / 2;
      let rotateX = ((y - centerY) / centerY) * 15;
      let rotateY = ((centerX - x) / centerX) * 15;

      if (e.clientX < offsetX + boundary || e.clientX > offsetX + activeWidth - boundary || e.clientY < offsetY + boundary || e.clientY > offsetY + activeHeight - boundary) {
        const distanceX = Math.min(e.clientX - offsetX, offsetX + activeWidth - e.clientX);
        const distanceY = Math.min(e.clientY - offsetY, offsetY + activeHeight - e.clientY);
        const distance = Math.min(distanceX, distanceY);
        const factor = Math.max(0, Math.min(1, distance / boundary));
        rotateX *= factor;
        rotateY *= factor;
      }

      card.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
      card.style.setProperty('--mouse-x', `${x}px`);
      card.style.setProperty('--mouse-y', `${y}px`);
    });
  });
</script>

<body>
  <div class="card-container">
    <div class="card">
      <div class="holographic-bg"></div>
      <div class="creditcard-content">
        <h1>Credit Card Details</h1>
      </div>
    </div>
  </div>
</body>

<style>
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
    width: 850px;
    height: 500px;
    background: black;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    transition: box-shadow 0.3s ease-in-out, background 0.3s ease-in-out;
    transform-style: preserve-3d;
    cursor: pointer;
    --mouse-x: 50%;
    --mouse-y: 50%;
    background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.05) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.05) 50%, rgba(255, 255, 255, 0.05) 75%, transparent 75%, transparent);
    background-size: 50px 50px;
  }
  .card:hover {
    background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.3) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.3) 50%, rgba(255, 255, 255, 0.3) 75%, transparent 75%, transparent);
  }
  .holographic-bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle at var(--mouse-x) var(--mouse-y), rgba(255, 255, 255, 0.5), rgba(0, 0, 255, 0.2), rgba(0, 0, 0, 0.3), rgba(0, 0, 255, 0.3));
    background-size: 200% 200%;
    transition: background-position 0.3s ease-in-out, opacity 0.3s ease-in-out;
    pointer-events: none;
    opacity: 0;
    z-index: 0;
  }
  .card:hover .holographic-bg {
    opacity: 1;
  }
  .creditcard-content {
    position: relative;
    display: flex;
    width: 100%;
    height: 100%;
    color: white;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    justify-content: center;
    align-items: center;
    z-index: 1;
  }
  @keyframes shimmer {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }
</style>