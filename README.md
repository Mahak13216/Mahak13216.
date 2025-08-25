<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic Product Filter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    .product-container {
      border: 1px solid #ccc;
      padding: 20px;
      margin-bottom: 30px;
      width: 300px;
    }
    .product {
      margin: 5px 0;
      padding: 5px;
      background-color: #f9f9f9;
    }
  </style>
</head>
<body>

  <div class="product-container">
    <h2>Product List</h2>
    <label for="categoryFilter">Filter by Category:</label>
    <select id="categoryFilter">
      <option value="All">All</option>
      <option value="Clothing">Clothing</option>
      <option value="Electronics">Electronics</option>
      <option value="Books">Books</option>
    </select>

    <div id="productList"></div>
  </div>

  <script>
    const products = [
      { name: "T-Shirt", category: "Clothing" },
      { name: "Jeans", category: "Clothing" },
      { name: "Headphones", category: "Electronics" },
      { name: "Smartphone", category: "Electronics" },
      { name: "Novel", category: "Books" },
      { name: "Cookbook", category: "Books" }
    ];

    const productList = document.getElementById('productList');
    const categoryFilter = document.getElementById('categoryFilter');

    function displayProducts(category) {
      productList.innerHTML = '';
      const filteredProducts = category === 'All' ? products : products.filter(p => p.category === category);
      filteredProducts.forEach(product => {
        const div = document.createElement('div');
        div.className = 'product';
        div.textContent = product.name;
        productList.appendChild(div);
      });
    }

    displayProducts('All');

    categoryFilter.addEventListener('change', function () {
      displayProducts(this.value);
    });
  </script>

</body>
</html>
