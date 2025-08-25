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




<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Live Character Counter</title>
  <style>
    body {
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      background: #f7f9fc;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      background: #fff;
      padding: 25px;
      border: 3px solid #010b16;
      border-radius: 15px;
      box-shadow: 0 6px 15px rgba(0, 0, 0, 0.15);
      width: 400px;
    }

    h2 {
      text-align: center;
      color: #010b15;
      margin-bottom: 20px;
    }

    textarea {
      width: 100%;
      height: 150px;
      padding: 12px;
      font-size: 16px;
      border: 2px solid #ccc;
      border-radius: 10px;
      outline: none;
      resize: none;
      box-sizing: border-box;
      transition: border-color 0.3s;
    }

    textarea:focus {
      border-color: #010a15;
      box-shadow: 0 0 6px rgba(30, 30, 30, 0.5);
    }

    .counter-box {
      margin-top: 12px;
      padding: 8px;
      text-align: center;
      font-size: 15px;
      border: 2px solid #010810;
      border-radius: 8px;
      background: #f1f8ff;
      font-weight: bold;
      color: #333;
    }

    .limit-reached {
      color: #d9534f;
      border-color: #d9534f;
      background: #ffe6e6;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Live Character Counter</h2>
    <textarea id="textInput" maxlength="200" placeholder="Type something..."></textarea>
    <div id="charCounter" class="counter-box">0 / 200 characters</div>
  </div>

  <script>
    const textarea = document.getElementById("textInput");
    const counter = document.getElementById("charCounter");
    const maxLength = textarea.getAttribute("maxlength");

    textarea.addEventListener("input", () => {
      const currentLength = textarea.value.length;
      counter.textContent = ${currentLength} / ${maxLength} characters;

      if (currentLength >= maxLength) {
        counter.classList.add("limit-reached");
      } else {
        counter.classList.remove("limit-reached");
      }
    });
  </script>
</body>
</html>





<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>SVG Drawing Tool</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    .container {
      border: 2px solid #444;
      padding: 20px;
      width: fit-content;
    }
    svg {
      border: 2px solid #aaa;
      background-color: #f9f9f9;
      cursor: crosshair;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>SVG Drawing Tool</h2>
    <svg id="drawingCanvas" width="600" height="400"></svg>
  </div>

  <script>
    const svg = document.getElementById("drawingCanvas");
    let isDrawing = false;
    let currentPath;

    svg.addEventListener("mousedown", (e) => {
      isDrawing = true;
      const { x, y } = getMousePosition(e);
      currentPath = document.createElementNS("http://www.w3.org/2000/svg", "path");
      currentPath.setAttribute("stroke", "blue");
      currentPath.setAttribute("stroke-width", "2");
      currentPath.setAttribute("fill", "none");
      currentPath.setAttribute("d", M ${x} ${y});
      svg.appendChild(currentPath);
    });

    svg.addEventListener("mousemove", (e) => {
      if (!isDrawing) return;
      const { x, y } = getMousePosition(e);
      const d = currentPath.getAttribute("d");
      currentPath.setAttribute("d", ${d} L ${x} ${y});
    });

    svg.addEventListener("mouseup", () => {
      isDrawing = false;
    });

    svg.addEventListener("mouseleave", () => {
      isDrawing = false;
    });

    function getMousePosition(evt) {
      const CTM = svg.getScreenCTM();
      return {
        x: (evt.clientX - CTM.e) / CTM.a,
        y: (evt.clientY - CTM.f) / CTM.d
      };
    }
  </script>

</body>
</html>
