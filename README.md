<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Site Interativo Animado</title>
  <style>
    :root {
      --bg: #f4f4f9;
      --text: #333;
      --primary: #4a90e2;
    }
    body.dark {
      --bg: #222;
      --text: #f4f4f9;
      --primary: #ff9800;
    }
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: var(--bg);
      color: var(--text);
      transition: background 0.3s, color 0.3s;
      overflow-x: hidden;
    }
    header {
      background: var(--primary);
      color: white;
      padding: 20px;
      text-align: center;
      transform: translateY(-100%);
      animation: slideDown 1s forwards;
    }
    nav {
      background: #333;
      padding: 10px;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeIn 1s 0.8s forwards;
    }
    nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
      font-weight: bold;
      position: relative;
    }
    nav a::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: -5px;
      width: 0%;
      height: 2px;
      background: var(--primary);
      transition: width 0.3s;
    }
    nav a:hover::after {
      width: 100%;
    }
    .menu-btn {
      display: none;
      background: var(--primary);
      color: white;
      border: none;
      padding: 10px 15px;
      cursor: pointer;
      font-size: 16px;
      margin: 10px auto;
      border-radius: 5px;
      transition: transform 0.2s;
    }
    .menu-btn:hover {
      transform: scale(1.1);
    }
    main {
      padding: 20px;
      max-width: 900px;
      margin: auto;
    }
    section {
      opacity: 0;
      transform: translateY(50px);
      transition: all 0.8s ease-out;
    }
    section.show {
      opacity: 1;
      transform: translateY(0);
    }
    .btn-dark {
      margin-top: 20px;
      padding: 10px 15px;
      background: var(--primary);
      border: none;
      color: white;
      font-size: 14px;
      border-radius: 5px;
      cursor: pointer;
      transition: transform 0.2s, background 0.3s;
    }
    .btn-dark:hover {
      transform: scale(1.1);
      background: #333;
    }
    footer {
      background: #222;
      color: white;
      text-align: center;
      padding: 15px;
      margin-top: 30px;
      opacity: 0;
      animation: fadeIn 1s 1.5s forwards;
    }
    .hidden {
      display: none;
    }
    @media (max-width: 600px) {
      .menu-btn {
        display: block;
      }
      nav {
        flex-direction: column;
        align-items: center;
      }
      nav a {
        margin: 10px 0;
      }
    }

    /* 🔥 Animações */
    @keyframes slideDown {
      to {
        transform: translateY(0);
      }
    }
    @keyframes fadeIn {
      to {
        opacity: 1;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>🌐 Site Interativo com Animações</h1>
    <p>Agora muito mais moderno!</p>
  </header>

  <button class="menu-btn">☰ Menu</button>
  <nav class="hidden">
    <a href="#">Início</a>
    <a href="#">Sobre</a>
    <a href="#">Serviços</a>
    <a href="#">Contato</a>
  </nav>

  <main>
    <section>
      <h2>Bem-vindo!</h2>
      <p>Este é um site com recursos interativos, responsivo e animado usando HTML, CSS e JavaScript.</p>
    </section>

    <section>
      <h3>Contador de Visitas</h3>
      <p>Você já visitou este site <span id="visitas">0</span> vezes.</p>
    </section>

    <section>
      <h3>Personalização</h3>
      <button class="btn-dark" id="toggleTheme">🌙 Mudar Tema</button>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 - Site Interativo Animado</p>
  </footer>

  <script>
    // Botão do menu (mobile)
    const menuBtn = document.querySelector(".menu-btn");
    const nav = document.querySelector("nav");

    menuBtn.addEventListener("click", () => {
      nav.classList.toggle("hidden");
    });

    // Tema claro/escuro
    const toggleBtn = document.getElementById("toggleTheme");
    toggleBtn.addEventListener("click", () => {
      document.body.classList.toggle("dark");
      toggleBtn.textContent = 
        document.body.classList.contains("dark") ? "☀️ Mudar Tema" : "🌙 Mudar Tema";
    });

    // Contador de visitas (localStorage)
    let visitas = localStorage.getItem("visitas") || 0;
    visitas++;
    localStorage.setItem("visitas", visitas);
    document.getElementById("visitas").textContent = visitas;

    // Animações com scroll
    const sections = document.querySelectorAll("section");
    function showSections() {
      const trigger = window.innerHeight * 0.8;
      sections.forEach(sec => {
        const top = sec.getBoundingClientRect().top;
        if (top < trigger) {
          sec.classList.add("show");
        }
      });
    }
    window.addEventListener("scroll", showSections);
    window.addEventListener("load", showSections);
  </script>
</body>
</html>
