document.addEventListener('DOMContentLoaded', function() {
    // Добавление товара в корзину
    const addToCartButtons = document.querySelectorAll('.add-to-cart');
    addToCartButtons.forEach(button => {
        button.addEventListener('click', function() {
            alert('Товар добавлен в корзину');
        });
    });
    
    // Фильтрация товаров в каталоге
    if (document.getElementById('category-filter')) {
        const categoryFilter = document.getElementById('category-filter');
        const searchInput = document.getElementById('search');
        const productCards = document.querySelectorAll('.product-card');
        
        function filterProducts() {
            const selectedCategory = categoryFilter.value;
            const searchText = searchInput.value.toLowerCase();
            
            productCards.forEach(card => {
                const category = card.getAttribute('data-category');
                const title = card.querySelector('h3').textContent.toLowerCase();
                const matchesCategory = selectedCategory === 'all' || category === selectedCategory;
                const matchesSearch = title.includes(searchText);
                
                if (matchesCategory && matchesSearch) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        }
        
        categoryFilter.addEventListener('change', filterProducts);
        searchInput.
addEventListener('input', filterProducts);
    }
    
    // Управление количеством товаров в корзине
    const decreaseButtons = document.querySelectorAll('.decrease');
    const increaseButtons = document.querySelectorAll('.increase');
    const removeButtons = document.querySelectorAll('.remove-item');
    
    decreaseButtons.forEach(button => {
        button.addEventListener('click', function() {
            const quantityElement = this.nextElementSibling;
            let quantity = parseInt(quantityElement.textContent);
            if (quantity > 1) {
                quantity--;
                quantityElement.textContent = quantity;
                updateCartItemPrice(this.closest('.cart-item'));
            }
        });
    });
    
    increaseButtons.forEach(button => {
        button.addEventListener('click', function() {
            const quantityElement = this.previousElementSibling;
            let quantity = parseInt(quantityElement.textContent);
            quantity++;
            quantityElement.textContent = quantity;
            updateCartItemPrice(this.closest('.cart-item'));
        });
    });
    
    removeButtons.forEach(button => {
        button.addEventListener('click', function() {
            this.closest('.cart-item').remove();
            updateCartSummary();
        });
    });
    
    function updateCartItemPrice(item) {
        const pricePerUnit = parseFloat(item.querySelector('.item-info p').textContent.match(/\d+/)[0]);
        const quantity = parseInt(item.querySelector('.quantity').textContent);
        const totalPrice = pricePerUnit * quantity;
        item.querySelector('.item-price span').textContent = totalPrice + ' руб.';
        updateCartSummary();
    }
    
    function updateCartSummary() {
        // Здесь должна быть логика обновления итоговой суммы
        // В реальном проекте это будет более сложная функция
    }
    
    // Обработка формы обратной связи
    if (document.getElementById('feedback-form')) {
        document.getElementById('feedback-form').addEventListener('submit', function(e) {
            e.preventDefault();
            alert('Спасибо за ваше сообщение! Мы свяжемся с вами в ближайшее время.');
            this.reset();
        });
    }
    
    // Обработка оформления заказа
    if (document.querySelector('.checkout-btn')) {
        document.querySelector('.checkout-btn').addEventListener('click', function() {
            alert('Заказ успешно оформлен! Спасибо за покупку.');
        });
    }
});
