# blog


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog Tech</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }

        header {
            background-color: #333;
            color: #fff;
            padding: 1em 0;
            text-align: center;
        }

      

      

      

        .categories button {
            background: none;
            border: none;
            color: white;
            margin-left: 1em;
            cursor: pointer;
        }

        .categories button:hover {
            text-decoration: underline;
        }

        .post-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
            padding: 2em;
        }

        .post-card {
            background: #f4f4f4;
            border: 1px solid #ddd;
            margin: 1em;
            padding: 1em;
            width: calc(33% - 2em);
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .post-card img {
            max-width: 100%;
            height: auto;
        }

        .post-card h2 {
            font-size: 1.5em;
            margin-top: 0;
        }

        .post-card p {
            color: #666;
        }

        .post-card .post-info {
            font-size: 0.9em;
            color: #999;
        }

        .post-content {
            padding: 2em;
        }

        .post-content h2 {
            font-size: 2em;
        }

        .post-content p {
            font-size: 1.2em;
            line-height: 1.6;
        }
    </style>
</head>
<body>
    <header>
        <nav>
            <h1>Blog Tech</h1>
           
        </nav>
    </header>
    <main>
        <div id="postContainer" class="post-container"></div>
        <div id="postContent" class="post-content" style="display:none;"></div>
    </main>
    <script>
        const posts = [
            {
                id: 1,
                title: "Pc Gamer",
                content: "Ryzen 5600x com rtx3060",
                date: "2024-01-01",
                image: "https://cdn.awsli.com.br/600x450/1742/1742668/produto/227496277/sem-t-tulo-1-7gowtxco3g.jpg",
                category: "programacao",
                views: 0
            },
            {
                id: 2,
                title: "Combo Escritorio",
                content: "Intel i5 3400 com placa amd integrada",
                date: "2024-02-01",
                image: "https://images.kabum.com.br/produtos/fotos/168396/computador-completo-intel-core-i5-2400-3-1ghz-8gb-ram-ddr3-ssd-240gb-teclado-e-mouse-monitor-19-preto_1661977101_gg.jpg",
                category: "hardware",
                views: 0
            },
           
        ];

        function loadPosts() {
            const postContainer = document.getElementById('postContainer');
            postContainer.innerHTML = '';
            posts.forEach(post => {
                const postCard = document.createElement('div');
                postCard.className = 'post-card';
                postCard.onclick = () => viewPost(post.id);
                postCard.innerHTML = `
                    <img src="${post.image}" alt="${post.title}">
                    <h2>${post.title}</h2>
                    <p>${post.content.substring(0, 100)}...</p>
                    <div class="post-info">
                        <span>${post.date}</span> | 
                        <span>${post.category}</span> | 
                        <span>${post.views} visualizações</span>
                    </div>
                `;
                postContainer.appendChild(postCard);
            });
        }

        function viewPost(id) {
            const post = posts.find(p => p.id === id);
            post.views += 1;
            localStorage.setItem('post', JSON.stringify(post));
            displayPost(post);
        }

        function displayPost(post) {
            const postContainer = document.getElementById('postContainer');
            const postContent = document.getElementById('postContent');
            postContainer.style.display = 'none';
            postContent.style.display = 'block';
            postContent.innerHTML = `
                <h2>${post.title}</h2>
                <img src="${post.image}" alt="${post.title}">
                <p>${post.content}</p>
                <div class="post-info">
                    <span>${post.date}</span> | 
                    <span>${post.category}</span> | 
                    <span>${post.views} visualizações</span>
                </div>
                <button onclick="goBack()">Voltar</button>
            `;
        }

        function goBack() {
            const postContainer = document.getElementById('postContainer');
            const postContent = document.getElementById('postContent');
            postContainer.style.display = 'flex';
            postContent.style.display = 'none';
            loadPosts();
        }

        function filterPosts(category) {
            const postContainer = document.getElementById('postContainer');
            postContainer.innerHTML = '';
            const filteredPosts = category === 'todas' ? posts : posts.filter(post => post.category === category);
            filteredPosts.forEach(post => {
                const postCard = document.createElement('div');
                postCard.className = 'post-card';
                postCard.onclick = () => viewPost(post.id);
                postCard.innerHTML = `
                    <img src="${post.image}" alt="${post.title}">
                    <h2>${post.title}</h2>
                    <p>${post.content.substring(0, 100)}...</p>
                    <div class="post-info">
                        <span>${post.date}</span> | 
                        <span>${post.category}</span> | 
                        <span>${post.views} visualizações</span>
                    </div>
                `;
                postContainer.appendChild(postCard);
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            loadPosts();
        });
    </script>
</body>
</html>
