<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>I Love Mangás</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background-color: #1c1c1c;
      color: #fff;
    }
    header {
      background-color: #111;
      padding: 1rem;
      text-align: center;
      font-size: 1.5rem;
      border-bottom: 2px solid #444;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 1rem;
    }
    header img {
      height: 50px;
    }
    #search {
      padding: 1rem;
      text-align: center;
    }
    #search input {
      padding: 0.5rem;
      width: 80%;
      max-width: 400px;
      border-radius: 5px;
      border: none;
    }
    main {
      padding: 2rem;
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 1rem;
    }
    .manga {
      background-color: #2c2c2c;
      padding: 1rem;
      border-radius: 8px;
      text-align: center;
      transition: transform 0.2s ease;
    }
    .manga:hover {
      transform: scale(1.05);
      cursor: pointer;
    }
    .manga img {
      max-width: 100%;
      border-radius: 4px;
    }
    .chapter-list, .reader {
      display: none;
      flex-direction: column;
      align-items: center;
      padding: 2rem;
    }
    .chapter {
      background-color: #333;
      margin: 0.5rem;
      padding: 1rem;
      border-radius: 6px;
      cursor: pointer;
      width: 100%;
      max-width: 400px;
      text-align: center;
    }
    .reader img {
      width: 100%;
      max-width: 600px;
      margin-bottom: 1rem;
      border-radius: 8px;
    }
    .back {
      margin-top: 1rem;
      color: #00bfff;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>
    <img src="/mnt/data/A_logo_for_a_manga_website_or_brand_named_\"I_Love_.png" alt="Logo I Love Mangás">
    <span>I Love Mangás</span>
  </header>

  <div id="search">
    <input type="text" id="searchInput" placeholder="Buscar mangá..." onkeyup="searchManga()">
  </div>

  <main id="main">
    <div class="manga" data-title="Manga 1" onclick="openChapters('manga1')">
      <img src="https://via.placeholder.com/200x280?text=Mang%C3%A1+1" alt="Mangá 1">
      <p>Mangá 1</p>
    </div>
    <div class="manga" data-title="Manga 2" onclick="openChapters('manga2')">
      <img src="https://via.placeholder.com/200x280?text=Mang%C3%A1+2" alt="Mangá 2">
      <p>Mangá 2</p>
    </div>
    <!-- Adicione mais mangás -->
  </main>

  <section id="chapters" class="chapter-list"></section>

  <section id="reader" class="reader">
    <img id="page" src="" alt="Página do Mangá">
    <div>
      <button onclick="prevPage()">Página Anterior</button>
      <button onclick="nextPage()">Próxima Página</button>
    </div>
    <div class="back" onclick="goBackToChapters()">&larr; Voltar aos capítulos</div>
  </section>

  <script>
    const mangas = {
      manga1: {
        title: "Mangá 1",
        chapters: {
          1: 5,
          2: 4
        }
      },
      manga2: {
        title: "Mangá 2",
        chapters: {
          1: 3,
          2: 6
        }
      }
    };

    let currentManga = '';
    let currentChapter = 1;
    let currentPage = 1;

    function searchManga() {
      const input = document.getElementById('searchInput').value.toLowerCase();
      const mangaCards = document.querySelectorAll('.manga');
      mangaCards.forEach(card => {
        const title = card.dataset.title.toLowerCase();
        card.style.display = title.includes(input) ? 'block' : 'none';
      });
    }

    function openChapters(mangaKey) {
      currentManga = mangaKey;
      const chapters = mangas[mangaKey].chapters;
      let html = `<h2>${mangas[mangaKey].title}</h2>`;
      for (const chapter in chapters) {
        html += `<div class="chapter" onclick="openChapter(${chapter})">Capítulo ${chapter}</div>`;
      }
      document.getElementById('chapters').innerHTML = html;
      document.getElementById('main').style.display = 'none';
      document.getElementById('chapters').style.display = 'flex';
    }

    function openChapter(chapter) {
      currentChapter = chapter;
      currentPage = 1;
      document.getElementById('chapters').style.display = 'none';
      document.getElementById('reader').style.display = 'flex';
      updatePage();
    }

    function updatePage() {
      document.getElementById('page').src = `https://via.placeholder.com/600x800?text=${currentManga}+Cap${currentChapter}+Pag${currentPage}`;
    }

    function nextPage() {
      const total = mangas[currentManga].chapters[currentChapter];
      if (currentPage < total) {
        currentPage++;
        updatePage();
      }
    }

    function prevPage() {
      if (currentPage > 1) {
        currentPage--;
        updatePage();
      }
    }

    function goBackToChapters() {
      document.getElementById('reader').style.display = 'none';
      document.getElementById('chapters').style.display = 'flex';
    }
  </script>
</body>
</html>
