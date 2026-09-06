<!DOCTYPE html>
<html lang="ckb" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Royal Shop - کاتالۆگی ئامێرەکانی ناوماڵ</title>
    <link href="https://fonts.googleapis.com/css2?family=Nrt&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0d0d0d;
            --card-bg: #181818;
            --accent-gold: #d4af37;
            --light-gold: #f4e0a5;
            --text-color: #ffffff;
            --subtext-color: #aaaaaa;
            --whatsapp-green: #25D366;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Nrt', Arial, sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-color); padding: 15px; direction: rtl; }
        header { background: linear-gradient(135deg, #111, #222); padding: 25px 15px; text-align: center; border-radius: 12px; border: 1px solid #333; margin-bottom: 20px; }
        header h1 { color: var(--accent-gold); font-size: 1.8rem; margin-bottom: 5px; text-transform: uppercase; letter-spacing: 1px; }
        header p { color: var(--subtext-color); font-size: 0.9rem; }
        .search-container { max-width: 600px; margin: 0 auto 15px auto; }
        .search-input { width: 100%; padding: 12px 18px; border-radius: 25px; border: 1px solid var(--accent-gold); background: #151515; color: #fff; font-size: 0.95rem; outline: none; }
        .categories-container { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 10px; margin-bottom: 20px; scrollbar-width: none; }
        .categories-container::-webkit-scrollbar { display: none; }
        .category-btn { background-color: #222; border: 1px solid #444; color: #ccc; padding: 8px 16px; border-radius: 20px; cursor: pointer; white-space: nowrap; font-size: 0.85rem; }
        .category-btn.active { background-color: var(--accent-gold); color: #000; font-weight: bold; border-color: var(--accent-gold); }
        .products-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 15px; }
        .product-card { background-color: var(--card-bg); border-radius: 10px; overflow: hidden; border: 1px solid #282828; display: flex; flex-direction: column; justify-content: space-between; }
        .product-img { width: 100%; height: 160px; object-fit: cover; background-color: #222; }
        .product-info { padding: 12px; text-align: center; }
        .product-title { font-size: 0.95rem; margin-bottom: 6px; color: var(--light-gold); font-weight: bold; }
        .product-price { font-size: 0.95rem; color: var(--accent-gold); font-weight: bold; margin-bottom: 10px; }
        .whatsapp-btn { display: block; background-color: var(--whatsapp-green); color: #fff; text-decoration: none; padding: 8px; border-radius: 6px; font-size: 0.85rem; font-weight: bold; text-align: center; }
        footer { text-align: center; margin-top: 30px; padding: 15px; color: var(--subtext-color); font-size: 0.85rem; border-top: 1px solid #222; }
        footer strong { color: var(--accent-gold); }
    </style>
</head>
<body>

    <header>
        <h1>ROYAL SHOP</h1>
        <p>شاهانەترین ئامێرەکانی ناوماڵ - هەولێر</p>
    </header>

    <div class="search-container">
        <input type="text" id="searchInput" class="search-input" placeholder="گەڕان بۆ ئامێرەکان..." oninput="filterProducts()">
    </div>

    <div class="categories-container">
        <button class="category-btn active" onclick="filterCategory('all', this)">هەموو بەرهەمەکان</button>
        <button class="category-btn" onclick="filterCategory('iron', this)">ئووتی</button>
        <button class="category-btn" onclick="filterCategory('dough_mixer', this)">عەجانە</button>
        <button class="category-btn" onclick="filterCategory('ice_crusher', this)">بەفر شکێن</button>
        <button class="category-btn" onclick="filterCategory('ice_maker', this)">بەفر دروستکەر</button>
        <button class="category-btn" onclick="filterCategory('juicer', this)">عەسارە</button>
        <button class="category-btn" onclick="filterCategory('mixer', this)">میکسەر</button>
        <button class="category-btn" onclick="filterCategory('meat_grinder', this)">مەکینەی گۆشت</button>
        <button class="category-btn" onclick="filterCategory('air_fryer', this)">قەلا</button>
        <button class="category-btn" onclick="filterCategory('vacuum', this)">گەسک</button>
        <button class="category-btn" onclick="filterCategory('coffee', this)">قاوە ساز</button>
        <button class="category-btn" onclick="filterCategory('rice_cooker', this)">ڕایس کوکەر</button>
        <button class="category-btn" onclick="filterCategory('chopper', this)">شکێنەر</button>
        <button class="category-btn" onclick="filterCategory('toaster', this)">جیهازی تۆست</button>
        <button class="category-btn" onclick="filterCategory('laser_stove', this)">تەباخی لێزەری</button>
        <button class="category-btn" onclick="filterCategory('scale', this)">تەرازوو</button>
        <button class="category-btn" onclick="filterCategory('egg_cooker', this)">جیهازی هێلکە</button>
        <button class="category-btn" onclick="filterCategory('shaver', this)">جیهازی شەندەری</button>
        <button class="category-btn" onclick="filterCategory('oven', this)">فرن</button>
        <button class="category-btn" onclick="filterCategory('mixer_set', this)">سێت میکسەر</button>
        <button class="category-btn" onclick="filterCategory('hair_dryer', this)">مجەففە</button>
        <button class="category-btn" onclick="filterCategory('kettle', this)">کتلی</button>
    </div>

    <div class="products-grid" id="productsGrid"></div>

    <footer>
        <p><strong>Royal Shop</strong> - هەولێر</p>
        <p>پەیوەندی: 07507284547 | 07504973235</p>
    </footer>

    <script>
        const whatsappNumber = "9647504973235";

        function generateItems(prefix, count, category, label) {
            let items = [];
            for (let i = 1; i <= count; i++) {
                items.push({
                    id: prefix * 100 + i,
                    name: `${label} مۆدێلی ${i}`,
                    price: "0$",
                    category: category,
                    image: "https://i.ibb.co/example.jpg"
                });
            }
            return items;
        }

        const products = [
            ...generateItems(1, 20, "iron", "ئووتی"),
            ...generateItems(2, 20, "dough_mixer", "عەجانە"),
            ...generateItems(3, 20, "ice_crusher", "بەفر شکێن"),
            ...generateItems(4, 20, "ice_maker", "بەفر دروستکەر"),
            ...generateItems(5, 20, "juicer", "عەسارە"),
            ...generateItems(6, 20, "mixer", "میکسەر"),
            ...generateItems(7, 20, "meat_grinder", "مەکینەی گۆشت"),
            ...generateItems(8, 20, "air_fryer", "قەلا"),
            ...generateItems(9, 20, "vacuum", "گەسک"),
            ...generateItems(10, 20, "coffee", "قاوە ساز"),
            ...generateItems(11, 20, "rice_cooker", "ڕایس کوکەر"),
            ...generateItems(12, 20, "chopper", "شکێنەر"),
            ...generateItems(13, 20, "toaster", "جیهازی تۆست"),
            ...generateItems(14, 20, "laser_stove", "تەباخی لێزەری"),
            ...generateItems(15, 20, "scale", "تەرازوو"),
            ...generateItems(16, 20, "egg_cooker", "جیهازی هێلکە"),
            ...generateItems(17, 20, "shaver", "جیهازی شەندەری"),
            ...generateItems(18, 20, "oven", "فرن"),
            ...generateItems(19, 20, "mixer_set", "سێت میکسەر"),
            ...generateItems(20, 20, "hair_dryer", "مجەففە"),
            ...generateItems(21, 20, "kettle", "کتلی")
        ];

        let selectedCategory = 'all';

        function renderProducts(items) {
            const grid = document.getElementById('productsGrid');
            grid.innerHTML = '';
            
            if (items.length === 0) {
                grid.innerHTML = '<p style="text-align:center; grid-column: 1/-1; color: #888; padding: 40px 0;">هیچ بەرهەمێک نەدۆزرایەوە.</p>';
                return;
            }

            items.forEach(product => {
                const message = encodeURIComponent(`سڵاو، داوای ئەم بەرهەمە دەکەم:\n\n*${product.name}*\nنرخ: ${product.price}`);
                const waLink = `https://wa.me/${whatsappNumber}?text=${message}`;

                const card = document.createElement('div');
                card.className = 'product-card';
                card.innerHTML = `
                    <img src="${product.image}" class="product-img" alt="${product.name}">
                    <div class="product-info">
                        <div class="product-title">${product.name}</div>
                        <div class="product-price">${product.price}</div>
                        <a href="${waLink}" target="_blank" class="whatsapp-btn">داواکردن لە واتسئاپ</a>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function filterProducts() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = products.filter(p => {
                const matchesCategory = selectedCategory === 'all' || p.category === selectedCategory;
                const matchesSearch = p.name.toLowerCase().includes(query);
                return matchesCategory && matchesSearch;
            });
            renderProducts(filtered);
        }

        function filterCategory(category, btnElement) {
            selectedCategory = category;
            document.querySelectorAll('.category-btn').forEach(btn => btn.classList.remove('active'));
            btnElement.classList.add('active');
            filterProducts();
        }

        renderProducts(products);
    </script>
</body>
</html>
        const products = [
            ...generateItems(1, 20, "iron", "ئووتی"),
            ...generateItems(2, 20, "dough_mixer", "عەجانە"),
            ...generateItems(3, 20, "ice_crusher", "بەفر شکێن"),
            ...generateItems(4, 20, "ice_maker", "بەفر دروستکەر"),
            ...generateItems(5, 20, "juicer", "عەسارە"),
            
            // بەشی میکسەر: یەکەم دانە وێنەی Kenwood دەبێت
            {
                id: 601,
                name: "میکسەری Kenwood",
                price: "0$",
                category: "mixer",
                image: "https://i.ibb.co/C3T4m0f1/37919.jpg"
            },
            ...generateItems(6, 19, "mixer", "میکسەر"),
            
            ...generateItems(7, 20, "meat_grinder", "مەکینەی گۆشت"),
            ...generateItems(8, 20, "air_fryer", "قەلا"),
            ...generateItems(9, 20, "vacuum", "گەسک"),
            ...generateItems(10, 20, "coffee", "قاوە ساز"),
            ...generateItems(11, 20, "rice_cooker", "ڕایس کوکەر"),
            ...generateItems(12, 20, "chopper", "شکێنەر"),
            ...generateItems(13, 20, "toaster", "جیهازی تۆست"),
            ...generateItems(14, 20, "laser_stove", "تەباخی لێزەری"),
            ...generateItems(15, 20, "scale", "تەرازوو"),
            ...generateItems(16, 20, "egg_cooker", "جیهازی هێلکە"),
            ...generateItems(17, 20, "shaver", "جیهازی شەندەری"),
            ...generateItems(18, 20, "oven", "فرن"),
            ...generateItems(19, 20, "mixer_set", "سێت میکسەر"),
            ...generateItems(20, 20, "hair_dryer", "مجەففە"),
            ...generateItems(21, 20, "kettle", "کتلی")
        ];
