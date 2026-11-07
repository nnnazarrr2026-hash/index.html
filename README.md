# index.html<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Цветочный рай</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #fdf8f0, #f9e8d9);
      color: #3d2b1f;
      line-height: 1.6;
    }

    header {
      background: #7a4c3c;
      color: #fff;
      padding: 20px 0;
      text-align: center;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    header h1 {
      font-size: 2.5rem;
      letter-spacing: 2px;
    }

    header p {
      font-size: 1.1rem;
      opacity: 0.9;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
    }

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      margin: 40px 0;
    }

    .flower-card {
      background: #fff;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 4px 15px rgba(0,0,0,0.08);
      transition: transform 0.3s;
    }

    .flower-card:hover {
      transform: translateY(-6px);
    }

    .flower-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      display: block;
    }

    .flower-info {
      padding: 15px;
    }

    .flower-info h3 {
      color: #7a4c3c;
      margin-bottom: 8px;
    }

    .flower-info .price {
      font-weight: bold;
      color: #b76e4a;
      font-size: 1.2rem;
    }

    .btn {
      display: inline-block;
      background: #7a4c3c;
      color: #fff;
      padding: 10px 20px;
      text-decoration: none;
      border-radius: 30px;
      border: none;
      cursor: pointer;
      font-size: 1rem;
      transition: background 0.2s;
      margin-top: 10px;
    }

    .btn:hover {
      background: #5f3a2e;
    }

    .order-form {
      background: #fff;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.08);
      max-width: 500px;
      margin: 40px auto;
    }

    .order-form input,
    .order-form textarea {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border: 1px solid #ddd;
      border-radius: 8px;
      font-size: 1rem;
    }

    .order-form textarea {
      height: 100px;
      resize: vertical;
    }

    footer {
      text-align: center;
      padding: 30px;
      background: #3d2b1f;
      color: #fff;
      margin-top: 40px;
    }

    footer a {
      color: #f9e8d9;
    }

    .contact-info {
      margin: 10px 0;
    }

    @media (max-width: 600px) {
      header h1 {
        font-size: 1.8rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>🌸 Цветочный рай</h1>
    <p>Свежие букеты с доставкой по городу</p>
  </header>

  <div class="container">
    <h2 style="text-align:center; margin-top: 20px;">Наши букеты</h2>
    <div class="gallery" id="gallery"></div>

    <h2 style="text-align:center; margin-top: 40px;">Заказать букет</h2>
    <div class="order-form">
      <form id="orderForm">
        <input type="text" name="name" placeholder="Ваше имя" required>
        <input type="tel" name="phone" placeholder="Телефон" required>
        <input type="email" name="email" placeholder="Email">
        <textarea name="comment" placeholder="Комментарий к заказу"></textarea>
        <button type="submit" class="btn">Отправить заказ</button>
      </form>
      <p id="formMessage" style="margin-top:10px; color:green;"></p>
    </div>

    <div style="text-align:center; margin: 30px 0;">
      <p>📞 +7 (999) 123-45-67</p>
      <p>📧 info@cveti-rai.ru</p>
      <p>📍 ул. Цветочная, 12</p>
    </div>
  </div>

  <footer>
    <p>© 2026 Цветочный рай | <a href="#">Политика конфиденциальности</a></p>
  </footer>

  <script>
    // Данные о цветах
    const flowers = [
      { name: 'Букет "Нежность"', desc: 'Розы, лилии, гипсофила', price: '2 500 ₽', img: 'https://images.unsplash.com/photo-1563241527-3004b7be0ffd?w=400' },
      { name: 'Букет "Солнечный"', desc: 'Подсолнухи, герберы, хризантемы', price: '2 000 ₽', img: 'https://images.unsplash.com/photo-1490750967868-88d9e8e5b0c4?w=400' },
      { name: 'Букет "Элегантность"', desc: 'Пионы, эустома, зелень', price: '3 200 ₽', img: 'https://images.unsplash.com/photo-1559561853-084c1ea8ba2c?w=400' },
      { name: 'Букет "Романтика"', desc: 'Альстромерии, ирисы, фрезии', price: '2 800 ₽', img: 'https://images.unsplash.com/photo-1582794543139-8ac9cb0f7b11?w=400' }
    ];

    const gallery = document.getElementById('gallery');

    flowers.forEach(flower => {
      const card = document.createElement('div');
      card.className = 'flower-card';
      card.innerHTML = `
        <img src="${flower.img}" alt="${flower.name}" loading="lazy">
        <div class="flower-info">
          <h3>${flower.name}</h3>
          <p>${flower.desc}</p>
          <p class="price">${flower.price}</p>
          <button class="btn" onclick="orderFlower('${flower.name}')">Заказать</button>
        </div>
      `;
      gallery.appendChild(card);
    });

    // Функция для быстрого заказа
    function orderFlower(name) {
      const form = document.getElementById('orderForm');
      form.querySelector('textarea').value = `Хочу заказать: ${name}`;
      form.querySelector('input[name="name"]').focus();
      window.scrollTo({ top: form.offsetTop - 20, behavior: 'smooth' });
    }

    // Обработка формы
    document.getElementById('orderForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const msg = document.getElementById('formMessage');
      msg.textContent = '✅ Спасибо! Мы свяжемся с вами в ближайшее время.';
      this.reset();
      setTimeout(() => msg.textContent = '', 5000);
    });
  </script>
</body>
</html>
