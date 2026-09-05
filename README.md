<button class="category-btn active" onclick="filterCategory('all', this)">هەموو بەرهەمەکان</button>
        <button class="category-btn" onclick="filterCategory('ئوتی', this)">ئوتی</button>
        <button class="category-btn" onclick="filterCategory('عەجانە', this)">عەجانە</button>
        <button class="category-btn" onclick="filterCategory('عەسارە', this)">عەسارە</button>
        <button class="category-btn" onclick="filterCategory('مەکینەی قاوە', this)">مەکینەی قاوە</button>
        <button class="category-btn" onclick="filterCategory('گسک', this)">گسک</button>
    </div>

    <div class="products-grid" id="productsGrid"></div>

    <footer>
        <p><strong>Royal Shop</strong> - هەولێر</p>
        <p>پەیوەندی: 07504973235 | 07507284547</p>
    </footer>

    <script>
        const whatsappNumber = "9647504973235";

        const products = [
            { id: 1, name: "عەجانەی هەویر 12 لیتر", category: "عەجانە", price: 100 دینار", image: "https://via.placeholder.com/300x300/181818/d4af37?text=عەجانە" },
            { id: 2, name: "مەکینەی قاوەی ئیسپڕێسۆ", category: "مەکینەی قاوە", price: "٦٥,٠٠٠ دینار", image: "https://via.placeholder.com/300x300/181818/d4af37?text=مەکینەی+قاوە" },
            { id: 3, name: "ئوتی هەڵمی پرۆفێشناڵ", category: "ئوتی", price: "٢٥,٠٠٠ دینار", image: "https://via.placeholder.com/300x300/181818/d4af37?text=ئوتی" },
            { id: 4, name: "عەسارەی میوەی فرێش", category: "عەسارە", price: "٣٥,٠٠٠ دینار", image: "https://via.placeholder.com/300x300/181818/d4af37?text=عەسارە" },
            { id: 5, name: "گسکی کارەبایی ٢٠٠٠ واٹ", category: "گسک", price: "٥٥,٠٠٠ دینار", image: "https://via.placeholder.com/300x300/181818/d4af37?text=گسک" }
        ];{ id: 1, name ئوتی راف ١٢١٥ 
const products = [
  { id: 1, name: "عەجانەی هەویر ٥ لیتر", price: "45$", category: "kitchen", image: "..." },
  { id: 2, name: "مەکینەی قهوەی ئیسپڕێسۆ", price: "35$", category: "coffee", image: "..." },
  { id: 3, name: "ئووتی هەڵمی پڕۆفێشناڵ", price: "25$", category: "home", image: "..." },
  { id: 4, name: "عەسارەی میوەی فرێش", price: "20$", category: "kitchen", image: "..." },
  { id: 5, name: "گسکی کارەبایی ۲۰۰ وات", price: "30$", category: "home", image: "..." },
  { id: 6, name: "ئووتی ڕاف ١٢١٥", price: "15$", category: "home", image: "لینکی وێنەکە" }
];

        let selectedCategory = 'all';

        function renderProducts(items) {
            const grid = document.getElementById('productsGrid');
            grid.innerHTML = '';
            if (items.length === 0) {
                grid.innerHTML = '<p style="text-align:center; grid-column: 1/-1; color: #888;">هیچ بەرهەمێک نەدۆزرایەوە</p>';
                return;
            }
            items.forEach(product => {
                const message = encodeURIComponent(`سڵاو Royal Shop، پرسیارم هەبوو دەربارەی: ${product.name}`);
                const waLink = `https://wa.me/${whatsappNumber}?text=${message}`;

                const card = document.createElement('div');
                card.className = 'product-card';
                card.innerHTML = `
                    <img src="${product.image}" alt="${product.name}" class="product-img">
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

