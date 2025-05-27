<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Super Duper Site</title>
  <style>
    :root {
      --bg: #ffffff;
      --text: #222;
      --primary: #007bff;
      --card-bg: #f9f9f9;
    }
    [data-theme="dark"] {
      --bg: #121212;
      --text: #e0e0e0;
      --primary: #00bfff;
      --card-bg: #1e1e1e;
    }

    * {
      box-sizing: border-box;
      scroll-behavior: smooth;
      transition: all 0.3s ease;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background: var(--bg);
      color: var(--text);
      margin: 0;
      line-height: 1.6;
    }

    header {
      background: var(--primary);
      color: #fff;
      padding: 1rem 20px;
      position: sticky;
      top: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    nav a {
      color: #fff;
      margin: 0 10px;
      text-decoration: none;
      font-weight: bold;
    }

    .theme-toggle {
      cursor: pointer;
      padding: 0.4em 0.8em;
      background: #fff;
      color: var(--primary);
      border: none;
      border-radius: 5px;
    }

    section {
      max-width: 1000px;
      margin: auto;
      padding: 60px 20px;
      opacity: 0;
      transform: translateY(50px);
    }

    section.visible {
      opacity: 1;
      transform: translateY(0);
    }

    .card {
      background: var(--card-bg);
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    .contact input, .contact textarea {
      width: 95%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }

    .contact button {
      background: var(--primary);
      color: #fff;
      padding: 10px 15px;
      margin-top: 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .carousel {
      display: flex;
      overflow: hidden;
      width: 100%;
      margin-top: 20px;
      position: relative;
    }

    .carousel-inner {
      display: flex;
      transition: transform 0.5s ease-in-out;
    }

    .carousel-item {
      min-width: 100%;
      padding: 20px;
      background: var(--card-bg);
      border-radius: 10px;
    }

    .back-to-top {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: var(--primary);
      color: #fff;
      padding: 10px;
      border-radius: 50%;
      cursor: pointer;
      display: none;
    }

    @media (max-width: 768px) {
      nav {
        flex-direction: column;
      }
      .carousel-item {
        font-size: 0.9rem;
      }
    }
  </style>
</head>
<body>

  <header>
    <div><strong>Desmond SuperSite</strong></div>
    <nav>
      <a href="#home">Home</a>
      <a href="#about">About</a>
      <a href="#testimonials">Testimonials</a>
      <a href="#contact">Contact</a>
    </nav>
    <button class="theme-toggle" onclick="toggleTheme()">Toggle Theme</button>
  </header>

  <section id="home">
    <h1>🚀 Welcome to My SuperSite</h1>
    <p>Created by the fullstack Wizard Himself</p>
    <div class="card">
      <h2>🔥 My Features</h2>
      <ul>
        <li>I am a web developer</li>
        <li>I am a web Designer</li>
        <li>I am a Fullstack Engineer</li>
        <li>And a Genius...</li>
      </ul>
    </div>
  </section>

  <section id="about">
    <h2>🧠 About Us</h2>
    <p>We craft blazing fast, modern websites with zero external dependencies.</p>
  </section>

  <section id="testimonials">
    <h2>💬 Testimonials</h2>
    <div class="carousel">
      <div class="carousel-inner" id="carouselInner">
        <div class="carousel-item">“This site is amazing! he is so good!” — Davido</div>
        <div class="carousel-item">“Desmond is so Brilliant.” — Wizkid</div>
        <div class="carousel-item">“He Is a Wizard With The Codes” — BurnaBoy</div>
      </div>
    </div>
  </section>

  <section id="contact" class="contact">
    <h2>📬 Contact Us On 08033255516</h2>
    <form onsubmit="return validateForm(event)">
      <input type="text" id="name" placeholder="Name" required />
      <input type="email" id="email" placeholder="Email" required />
      <textarea id="message" placeholder="Message" rows="4" required></textarea>
      <button type="submit">Send</button>
      <p id="formFeedback" style="margin-top:10px;"></p>
    </form>
  </section>

  <div class="back-to-top" id="topBtn" onclick="scrollToTop()">↑</div>

  <script>
    // Theme toggle
    function toggleTheme() {
      const theme = document.body.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
      document.body.setAttribute('data-theme', theme);
    }

    // Animate sections on scroll
    const observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add("visible");
        }
      });
    }, { threshold: 0.1 });

    document.querySelectorAll("section").forEach(sec => observer.observe(sec));

    // Carousel logic
    let carouselIndex = 0;
    const carousel = document.getElementById('carouselInner');
    setInterval(() => {
      carouselIndex = (carouselIndex + 1) % 3;
      carousel.style.transform = `translateX(-${carouselIndex * 100}%)`;
    }, 3000);

    // Contact form validation
    function validateForm(e) {
      e.preventDefault();
      const name = document.getElementById("name").value.trim();
      const email = document.getElementById("email").value.trim();
      const msg = document.getElementById("message").value.trim();
      const feedback = document.getElementById("formFeedback");

      if (name.length < 2) {
        feedback.textContent = "Name must be at least 2 characters.";
        return false;
      }
      if (!email.includes("@")) {
        feedback.textContent = "Enter a valid email.";
        return false;
      }
      feedback.textContent = `Thanks, ${name}! We'll be in touch.`;
      e.target.reset();
      return false;
    }

    // Back to top button
    const topBtn = document.getElementById("topBtn");
    window.onscroll = () => {
      topBtn.style.display = window.scrollY > 300 ? "block" : "none";
    };
    function scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  </script>
</body>
</html>
