<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SmartStart — Инвестиции</title>
    <style>
        body {
            margin: 0;
            background: #0e0e0e;
            color: #e8e8e8;
            font-family: Arial, sans-serif;
        }

        header {
            display: flex;
            justify-content: space-between;
            padding: 20px;
            background: #161616;
        }

        .logo {
            color: #fff;
            font-size: 28px;
        }

        nav a {
            color: #aaa;
            margin-left: 20px;
            text-decoration: none;
        }

        nav a:hover {
            color: #fff;
        }

        .hero {
            text-align: center;
            padding: 80px 20px;
        }

        .features {
            display: flex;
            justify-content: space-around;
            padding: 40px;
        }

        .feature {
            background: #1c1c1c;
            padding: 20px;
            width: 30%;
            border-radius: 8px;
        }

        .asset-list {
            padding: 20px;
        }

        .asset-item {
            padding: 15px;
            background: #1a1a1a;
            margin-bottom: 15px;
            border-radius: 6px;
        }

        .asset-item:hover {
            background: #222;
            cursor: pointer;
        }

        footer {
            text-align: center;
            padding: 10px;
            background: #161616;
            color: #aaa;
        }

        select, button {
            padding: 10px;
            background: #333;
            color: #fff;
            border: none;
            border-radius: 6px;
        }

        select:focus, button:focus {
            outline: none;
        }
    </style>
</head>
<body>

<header>
    <h1 class="logo">СмартСтарт</h1>
    <nav>
        <a href="javascript:void(0);" onclick="showPage('home')">Главная</a>
        <a href="javascript:void(0);" onclick="showPage('investments')">Инвестиции</a>
        <a href="javascript:void(0);" onclick="showPage('premium')">Рекомендации</a>
    </nav>
</header>

<section id="home" style="display: block;">
    <div class="hero">
        <h2>Все инвестиционные возможности в одном месте</h2>
        <p>Криптовалюты, компании, стартапы — графики цен и аналитика.</p>
    </div>

    <div class="features">
        <div class="feature">
            <h3>📊 Графики цен</h3>
            <p>Просматривайте динамику активов в реальном времени.</p>
        </div>
        <div class="feature">
            <h3>📁 Категории</h3>
            <p>Экология, медицина, строительство, криптовалюты и другое.</p>
        </div>
        <div class="feature">
            <h3>💡 Рекомендации (подписка)</h3>
            <p>Получайте советы: покупать, держать или продавать.</p>
        </div>
    </div>
</section>

<section id="investments" style="display: none;">
    <h2 class="page-title">Список доступных активов</h2>
    <div class="filters">
        <select id="categoryFilter">
            <option value="all">Все категории</option>
            <option value="crypto">Криптовалюты</option>
            <option value="eco">Экология</option>
            <option value="med">Медицина</option>
            <option value="build">Строительство</option>
            <option value="startup">Стартапы</option>
        </select>
    </div>

    <div id="assetList" class="asset-list"></div>
</section>

<section id="premium" style="display: none;">
    <div id="content"></div>
</section>

<footer>
    SmartStart © 2025
</footer>

<script>
    const assets = [
        { "name": "Bitcoin", "symbol": "BTC", "category": "crypto" },
        { "name": "Ethereum", "symbol": "ETH", "category": "crypto" },
        { "name": "Tesla", "symbol": "TSLA", "category": "eco" },
        { "name": "Pfizer", "symbol": "PFE", "category": "med" },
        { "name": "EcoBuild Startup", "symbol": "ECOB", "category": "startup" }
    ];

    function showPage(page) {
        document.getElementById("home").style.display = "none";
        document.getElementById("investments").style.display = "none";
        document.getElementById("premium").style.display = "none";

        if (page === "home") {
            document.getElementById("home").style.display = "block";
        } else if (page === "investments") {
            document.getElementById("investments").style.display = "block";
            renderAssets(assets);
        } else if (page === "premium") {
            document.getElementById("premium").style.display = "block";
            loadPremiumContent();
        }
    }

    function renderAssets(list) {
        const container = document.getElementById("assetList");
        container.innerHTML = "";

        list.forEach(a => {
            const div = document.createElement("div");
            div.className = "asset-item";
            div.innerHTML = `<strong>${a.name}</strong> (${a.symbol})`;
            div.onclick = () => {
                window.location.href = `#${a.symbol}`;
            };
            container.appendChild(div);
        });
    }

    document.getElementById("categoryFilter").addEventListener("change", function () {
        const value = this.value;
        const filtered = value === "all" ? assets : assets.filter(a => a.category === value);
        renderAssets(filtered);
    });

    function loadPremiumContent() {
        const paid = localStorage.getItem("premium");

        const content = document.getElementById("content");

        if (paid === "yes") {
            content.innerHTML = `
                <h2>Рекомендации SmartStart</h2>
                <p>• Bitcoin — лучше подождать ✔</p>
                <p>• Tesla — хорошая возможность для покупки ✔</p>
            `;
        } else {
            content.innerHTML = `
                <h2>Рекомендации доступны по подписке</h2>
                <p>49$/мес</p>
                <button onclick="buy()">Оформить подписку</button>
            `;
        }
    }

    function buy() {
        localStorage.setItem("premium", "yes");
        loadPremiumContent();
    }

    // Для начальной загрузки страницы
    showPage("home");
</script>

</body>
</html>
