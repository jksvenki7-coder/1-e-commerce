# 1-e-commerce<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>JKS Group of Business</title>
<style>
  body {
    font-family: Arial, sans-serif;
    margin:0; padding:0; background: #f0f8ff;
    color:#333;
  }
  header, nav, main, footer {
    padding:10px 20px;
  }
  header {
    background: #87ceeb;
    color: white;
    text-align:center;
    font-size: 1.8em;
    font-weight: bold;
  }
  nav {
    background: #e0f0ff;
    display:flex;
    justify-content: space-around;
  }
  nav button {
    background: transparent;
    border:none;
    font-size: 1em;
    padding: 10px;
    cursor:pointer;
    color:#0077cc;
  }
  nav button:hover, nav button.active {
    color: #004080;
    font-weight:bold;
  }
  main {
    min-height: 70vh;
    padding: 20px;
    background: white;
  }
  .hidden { display:none; }
  .category-list, .product-list, .cart-list {
    list-style:none;
    padding: 0;
  }
  .category-list li, .product-list li {
    border: 1px solid #ddd;
    margin: 5px 0px;
    padding: 8px;
    cursor: pointer;
    border-radius: 5px;
  }
  .category-list li:hover, .product-list li:hover {
    background: #cce6ff;
  }
  .cart-list li {
    border-bottom: 1px dotted #aaa;
    padding: 5px 0;
  }
  .btn-primary {
    background-color: #0077cc;
    border: none;
    color: white;
    padding: 8px 15px;
    margin: 10px 0;
    cursor: pointer;
    border-radius: 5px;
  }
  input[type="number"] {
    width: 60px;
    margin-left: 10px;
    padding: 4px;
  }
  label {
    font-weight: bold;
  }
  form > div {
    margin: 5px 0;
  }
  #order-summary {
    margin-top: 20px;
    background: #eef9ff;
    padding: 10px;
    border-radius: 5px;
  }
  .camera-container video, .camera-container canvas {
    width: 100%;
    max-width: 400px;
    border-radius: 5px;
  }
  .map-container {
    width: 100%;
    height: 300px;
    border-radius: 5px;
  }
</style>
</head>
<body>

<header>JKS Group of Business</header>

<nav>
  <button id="nav-home" class="active">Home</button>
  <button id="nav-camera">Camera</button>
  <button id="nav-maps">Google Maps</button>
  <button id="nav-profile">Profile</button>
  <button id="nav-wallet">Wallet</button>
</nav>

<main>
  <!-- Home/Dashboard -->
  <section id="home-section">
    <h2>Welcome to JKS Group of Business</h2>
    <p>Select from the services below on the navigation bar.</p>
    <button id="start-ecommerce" class="btn-primary">Start E-commerce</button>
  </section>

  <!-- E-commerce -->
  <section id="ecommerce-section" class="hidden">
    <h2>E-commerce</h2>
    <!-- Main Categories -->
    <div>
      <label><strong>Categories:</strong></label>
      <ul id="main-category-list" class="category-list"></ul>
    </div>
    <!-- Subcategories -->
    <div id="subcategory-container" style="margin-top: 15px;"></div>

    <!-- Products -->
    <div id="product-container" style="margin-top:20px;"></div>

    <!-- Cart and Submit -->
    <div id="cart-container" style="margin-top:30px;">
      <h3>Cart</h3>
      <ul id="cart-list" class="cart-list"></ul>
      <button id="submit-order" class="btn-primary" disabled>Submit Order via WhatsApp</button>
    </div>

    <!-- Customer Details Form -->
    <div id="customer-details-container" class="hidden" style="margin-top:20px;">
      <h3>Enter Your Details</h3>
      <form id="customer-details-form">
        <div><label>Name:</label><input type="text" id="cust-name" required /></div>
        <div><label>Mobile Number:</label><input type="tel" id="cust-mobile" required pattern="^\+?\d{10,15}$" placeholder="+919876543210" /></div>
        <div><label>Delivery Address:</label><textarea id="cust-address" required rows="3"></textarea></div>
        <button type="submit" class="btn-primary">Send Order</button>
      </form>
    </div>

    <div id="order-summary"></div>
  </section>

  <!-- Camera Section -->
  <section id="camera-section" class="hidden">
    <h2>Camera Access</h2>
    <div class="camera-container">
      <video id="camera-video" autoplay></video>
      <canvas id="camera-canvas" class="hidden"></canvas>
      <button id="capture-photo" class="btn-primary">Capture Photo</button>
      <button id="retake-photo" class="btn-primary hidden">Retake</button>
      <div id="photo-result"></div>
    </div>
  </section>

  <!-- Maps Section -->
  <section id="maps-section" class="hidden">
    <h2>Google Maps</h2>
    <p>Your current location:</p>
    <div id="map" class="map-container"></div>
  </section>

  <!-- Profile Section -->
  <section id="profile-section" class="hidden">
    <h2>Profile</h2>
    <p>This is your user profile.</p>
  </section>

  <!-- Wallet Section -->
  <section id="wallet-section" class="hidden">
    <h2>Wallet</h2>
    <p>Manage your wallet and transactions here.</p>
  </section>

</main>

<script>
  // Sample data for categories, subcategories, and products per your requirements
  const ecommerceData = {
    "Groceries": {
      "Provisions": {
        "My Provisions": {
          "categories": ["Rice", "Dal", "Spices & Powders", "Oil", "Batters"],
          "items": {
            "Rice": ["Sona Masoori", "Idli Rice", "Basmati Rice"],
            "Dal": ["Toor Dal", "Moong Dal", "Udad Dal"],
            "Spices & Powders": ["Chilli Powder", "Coriander Powder", "Garam Masala"],
            "Oil": ["Sunflower Oil", "Palm Oil", "Groundnut Oil"],
            "Batters": ["Idli Batter", "Dosa Batter", "Pesarattu Batter"]
          }
        },
        "All Provisions": {
          "categories": ["Rice", "Dal", "Atta & Masala Items", "Oil and Ghee", "Batters & Sauces"],
          "items": {
            "Rice": ["Sona Masoori", "Idli Rice", "Basmati Rice"],
            "Dal": ["Toor Dal", "Moong Dal", "Udad Dal"],
            "Atta & Masala Items": ["Wheat Atta", "Maida", "Chili Powder", "Curry Powder"],
            "Oil and Ghee": ["Sunflower Oil", "Mustard Oil", "Ghee"],
            "Batters & Sauces": ["Idli Batter", "Dosa Batter", "Tomato Sauce"]
          }
        }
      },
      "Meat": {
        "categories": ["Chicken", "Mutton", "Fishes", "Crabs", "Eggs", "Others"],
        "items": {
          "Chicken": ["Boiler Chicken", "Country Chicken", "Farm Chicken", "Black Chicken", "Layer Chicken"],
          "Mutton": ["Head", "Legs", "Bone", "Boneless", "Mixed", "Liver", "Dhomma", "Blood", "Intestines"],
          "Fishes": ["Jeelabi", "Koramenu", "Chenduva"],
          "Prawns": ["Prawns"],
          "Crabs": ["Crabs"],
          "Eggs": ["Boiler Eggs", "Country Eggs"]
        },
        "partsChicken": ["Body Part", "Leg Part", "Mixed"],
        "muttonParts": ["Head", "Legs", "Bone", "Boneless", "Mixed", "Liver", "Dhomma", "Blood", "Intestines"]
      },
      "Milk": {
        "items": ["Milk", "Curd", "Ghee", "Paneer", "Butter", "Buttermilk"]
      },
      "Fruits & Vegetables": {
        "categories": ["Fruits", "Vegetables"],
        "items": {
          "Fruits": ["Mango", "Banana", "Apple", "Orange", "Grapes"],
          "Vegetables": ["Tomato", "Potato", "Onion", "Carrot", "Bitter Gourd"]
        }
      },
      "Flowers": {
        "items": ["Rose", "Jasmine", "Marigold", "Lotus"]
      },
      "Sweets and Drinks": {
        "categories": ["Snacks", "Drinks"],
        "items": {
          "Snacks": ["Lays", "Moong Dal", "Kurkure"],
          "Drinks": ["Thumsup", "Mirinda", "Sprite", "Red Bull", "Monster", "Jil Jeera"]
        }
      },
      "Others": {}
    }
  };

  // Global variables for selected data
  let currentMainCategory = null;
  let currentSubCategory = null;
  let currentProductCategory = null;
  let currentProducts = [];
  let cart = [];

  // Navigation buttons
  const navHome = document.getElementById('nav-home');
  const navCamera = document.getElementById('nav-camera');
  const navMaps = document.getElementById('nav-maps');
  const navProfile = document.getElementById('nav-profile');
  const navWallet = document.getElementById('nav-wallet');

  // Sections
  const homeSection = document.getElementById('home-section');
  const ecommerceSection = document.getElementById('ecommerce-section');
  const cameraSection = document.getElementById('camera-section');
  const mapsSection = document.getElementById('maps-section');
  const profileSection = document.getElementById('profile-section');
  const walletSection = document.getElementById('wallet-section');

  // E-commerce elements
  const mainCategoryList = document.getElementById('main-category-list');
  const subcategoryContainer = document.getElementById('subcategory-container');
  const productContainer = document.getElementById('product-container');
  const cartList = document.getElementById('cart-list');
  const submitOrderBtn = document.getElementById('submit-order');
  const customerDetailsContainer = document.getElementById('customer-details-container');
  const customerDetailsForm = document.getElementById('customer-details-form');
  const orderSummary = document.getElementById('order-summary');

  // Initialize app and event handlers
  function init() {
    navHome.addEventListener('click', () => showSection('home'));
    navCamera.addEventListener('click', () => showSection('camera'));
    navMaps.addEventListener('click', () => showSection('maps'));
    navProfile.addEventListener('click', () => showSection('profile'));
    navWallet.addEventListener('click', () => showSection('wallet'));
    document.getElementById('start-ecommerce').addEventListener('click', startEcommerce);

    submitOrderBtn.addEventListener('click', promptCustomerDetails);
    customerDetailsForm.addEventListener('submit', handleOrderSubmit);

    showSection('home');
    populateMainCategories();
  }

  function showSection(section) {
    homeSection.classList.add('hidden');
    ecommerceSection.classList.add('hidden');
    cameraSection.classList.add('hidden');
    mapsSection.classList.add('hidden');
    profileSection.classList.add('hidden');
    walletSection.classList.add('hidden');

    navHome.classList.remove('active');
    navCamera.classList.remove('active');
    navMaps.classList.remove('active');
    navProfile.classList.remove('active');
    navWallet.classList.remove('active');

    if (section === 'home') {
      homeSection.classList.remove('hidden');
      navHome.classList.add('active');
    } else if (section === 'camera') {
      cameraSection.classList.remove('hidden');
      navCamera.classList.add('active');
      startCamera();
    } else if (section === 'maps') {
      mapsSection.classList.remove('hidden');
      navMaps.classList.add('active');
      initMap();
    } else if (section === 'profile') {
      profileSection.classList.remove('hidden');
      navProfile.classList.add('active');
    } else if (section === 'wallet') {
      walletSection.classList.remove('hidden');
      navWallet.classList.add('active');
    } else if (section === 'ecommerce') {
      ecommerceSection.classList.remove('hidden');
    }
  }

  function startEcommerce() {
    showSection('ecommerce');
    clearEcommerceUI();
    currentMainCategory = 'Groceries';
    loadMainCategory(currentMainCategory);
  }

  function clearEcommerceUI() {
    mainCategoryList.innerHTML = '';
    subcategoryContainer.innerHTML = '';
    productContainer.innerHTML = '';
    cartList.innerHTML = '';
    orderSummary.innerHTML = '';
    customerDetailsContainer.classList.add('hidden');
    submitOrderBtn.disabled = true;
    cart = [];
  }

  // Populate main categories for e-commerce
  function populateMainCategories() {
    mainCategoryList.innerHTML = '';
    const categories = Object.keys(ecommerceData['Groceries']);
    for (const cat of categories) {
      let li = document.createElement('li');
      li.textContent = cat;
      li.addEventListener('click', () => loadCategory(cat));
      mainCategoryList.appendChild(li);
    }
  }

  // Load selected main category items (Provisions, Meat, etc.)
  function loadCategory(categoryName) {
    currentSubCategory = categoryName;
    subcategoryContainer.innerHTML = '';
    productContainer.innerHTML = '';

    const categoryData = ecommerceData['Groceries'][categoryName];
    if (!categoryData) return;

    // If category has subcategories or items
    if (categoryData.categories) {
      // Show subcategories
      let ul = document.createElement('ul');
      ul.className = 'category-list';
      for (const subcat of categoryData.categories) {
        let li = document.createElement('li');
        li.textContent = subcat;
        li.addEventListener('click', () => loadProducts(categoryName, subcat));
        ul.appendChild(li);
      }
      subcategoryContainer.innerHTML = `<h3>Select a category under ${categoryName}</h3>`;
      subcategoryContainer.appendChild(ul);
    } else if (categoryData.items) {
      // If just items array
      showProducts(categoryData.items);
    } else if (categoryData.items instanceof Array) {
      showProducts(categoryData.items);
    }
  }

  // Load products for categoryName -> subcatName
  function loadProducts(mainCat, subcatName) {
    productContainer.innerHTML = '';
    currentProductCategory = subcatName;
    let items = [];

    if (mainCat === 'Provisions') {
      items = ecommerceData['Groceries'][mainCat][subcatName]?.items || {};
      if (!items) return;
      showCategoryItems(items);
    } else if (mainCat === 'Meat') {
      items = ecommerceData['Groceries']['Meat'].items[subcatName] || [];
      // Special handling for Chicken or Mutton parts weight selections here
      showProductsWithOptions(subcatName, items);
    } else if (mainCat === 'Milk') {
      items = ecommerceData['Groceries']['Milk'].items || [];
      showProductsList(items);
    } else if (mainCat === 'Fruits & Vegetables' || mainCat === 'Sweets and Drinks') {
      let containerData = ecommerceData['Groceries'][mainCat];
      if (containerData.items && containerData.items[subcatName]) {
        showProductsList(containerData.items[subcatName]);
      }
    } else if (mainCat === 'Flowers') {
      let flowerItems = ecommerceData['Groceries']['Flowers'].items || [];
      showProductsList(flowerItems);
    }
  }

  // Show products under multiple categories e.g., Provisions->My Provisions->Rice->items as lists and add to cart options
  function showCategoryItems(items) {
    productContainer.innerHTML = '';
    let allCategories = Object.keys(items);
    for (const cat of allCategories) {
      let h4 = document.createElement('h4');
      h4.textContent = cat;
      productContainer.appendChild(h4);

      let ul = document.createElement('ul');
      ul.className = 'product-list';

      items[cat].forEach(prod => {
        let li = document.createElement('li');
        li.textContent = prod;

        let addButton = document.createElement('button');
        addButton.textContent = 'Select';
        addButton.style.marginLeft = "15px";
        addButton.onclick = () => addToCart(prod, 1);

        li.appendChild(addButton);
        ul.appendChild(li);
      });
      productContainer.appendChild(ul);
    }
  }

  // Show products in list form with add to cart and quantity
  function showProductsList(items) {
    productContainer.innerHTML = '';
    let ul = document.createElement('ul');
    ul.className = 'product-list';
    items.forEach(p => {
      let li = document.createElement('li');
      li.textContent = p + " ";
      let qtyInput = document.createElement('input');
      qtyInput.type = 'number';
      qtyInput.min = 1;
      qtyInput.value = 1;
      qtyInput.style.width = '50px';

      let addButton = document.createElement('button');
      addButton.textContent = 'Add to Cart';
      addButton.style.marginLeft = "10px";
      addButton.onclick = () => addToCart(p, parseInt(qtyInput.value));

      li.appendChild(qtyInput);
      li.appendChild(addButton);
      ul.appendChild(li);
    });
    productContainer.appendChild(ul);
  }

  // Show products with special handling for meat parts and weight entry
  function showProductsWithOptions(category, items) {
    productContainer.innerHTML = '';
    let ul = document.createElement('ul');
    ul.className = 'product-list';

    items.forEach(item => {
      let li = document.createElement('li');
      
      // Product name
      let nameSpan = document.createElement('span');
      nameSpan.textContent = item;
      li.appendChild(nameSpan);

      // For Chicken, batch select parts Body/Leg or Mixed
      if (category === 'Chicken') {
        let selectPart = document.createElement('select');
        selectPart.style.marginLeft = '10px';
        ['Body Part', 'Leg Part', 'Mixed'].forEach(p => {
          let option = document.createElement('option');
          option.value = p;
          option.textContent = p;
          selectPart.appendChild(option);
        });
        li.appendChild(selectPart);

        let weightInput = document.createElement('input');
        weightInput.type = 'number';
        weightInput.min = 250;
        weightInput.value = 250;
        weightInput.style.width = '80px';
        weightInput.style.marginLeft = '10px';
        li.appendChild(weightInput);

        let addButton = document.createElement('button');
        addButton.textContent = 'Add to Cart';
        addButton.style.marginLeft = "10px";
        addButton.onclick = () => {
          let part = selectPart.value;
          let weight = parseInt(weightInput.value);
          addToCart(item + ' (' + part + ')', weight);
        };
        li.appendChild(addButton);
      }
      // For Mutton similarly
      else if (category === 'Mutton') {
        let selectPart = document.createElement('select');
        selectPart.style.marginLeft = '10px';
        ecommerceData['Groceries']['Meat'].muttonParts.forEach(p => {
          let option = document.createElement('option');
          option.value = p;
          option.textContent = p;
          selectPart.appendChild(option);
        });
        li.appendChild(selectPart);

        let weightInput = document.createElement('input');
        weightInput.type = 'number';
        weightInput.min = 250;
        weightInput.value = 250;
        weightInput.style.width = '80px';
        weightInput.style.marginLeft = '10px';
        li.appendChild(weightInput);

        let addButton = document.createElement('button');
        addButton.textContent = 'Add to Cart';
        addButton.style.marginLeft = "10px";
        addButton.onclick = () => {
          let part = selectPart.value;
          let weight = parseInt(weightInput.value);
          addToCart(item + ' (' + part + ')', weight);
        };
        li.appendChild(addButton);
      }
      // For Fish, Prawns, Crabs - only weight input
      else if (['Fishes', 'Prawns', 'Crabs'].includes(category)) {
        let weightInput = document.createElement('input');
        weightInput.type = 'number';
        weightInput.min = 250;
        weightInput.value = 250;
        weightInput.style.width = '80px';
        weightInput.style.marginLeft = '10px';
        li.appendChild(weightInput);

        let addButton = document.createElement('button');
        addButton.textContent = 'Add to Cart';
        addButton.style.marginLeft = "10px";
        addButton.onclick = () => {
          let weight = parseInt(weightInput.value);
          addToCart(item, weight);
        };
        li.appendChild(addButton);
      }
      // For Eggs quantity selector (1 to 30)
      else if (category === 'Eggs') {
        let qtyInput = document.createElement('input');
        qtyInput.type = 'number';
        qtyInput.min = 1;
        qtyInput.max = 30;
        qtyInput.value = 1;
        qtyInput.style.width = '50px';
        qtyInput.style.marginLeft = '10px';
        li.appendChild(qtyInput);

        let addButton = document.createElement('button');
        addButton.textContent = 'Add to Cart';
        addButton.style.marginLeft = "10px";
        addButton.onclick = () => {
          let qty = parseInt(qtyInput.value);
          addToCart(item, qty);
        };
        li.appendChild(addButton);
      }
      else {
        // Fallback no options: just add to cart
        let addButton = document.createElement('button');
        addButton.textContent = 'Add to Cart';
        addButton.style.marginLeft = "10px";
        addButton.onclick = () => addToCart(item, 1);
        li.appendChild(addButton);
      }
      ul.appendChild(li);
    });

    productContainer.appendChild(ul);
  }

  // Add product to Cart Array and update UI
  function addToCart(productName, quantity) {
    if(quantity < 1){
      alert("Quantity/Weight must be at least 1.");
      return;
    }
    const cartItemIndex = cart.findIndex(item => item.name === productName);
    if (cartItemIndex >= 0) {
      cart[cartItemIndex].quantity += quantity;
    } else {
      cart.push({name: productName, quantity});
    }
    refreshCartUI();
  }

  // Refresh cart UI list and enable submit if at least one item
  function refreshCartUI() {
    cartList.innerHTML = '';
    for (const item of cart) {
      let li = document.createElement('li');
      li.textContent = `${item.name} - ${item.quantity}`;
      cartList.appendChild(li);
    }
    submitOrderBtn.disabled = cart.length === 0;
  }

  // Show customer details form for order submission
  function promptCustomerDetails() {
    customerDetailsContainer.classList.remove('hidden');
  }

  // Handle order submission: prepare WhatsApp message with cart and user information
  function handleOrderSubmit(e) {
    e.preventDefault();
    const name = document.getElementById('cust-name').value.trim();
    const mobile = document.getElementById('cust-mobile').value.trim();
    const address = document.getElementById('cust-address').value.trim();

    if (!name || !mobile || !address) {
      alert('Please fill all details.');
      return;
    }
    if (cart.length === 0) {
      alert('Cart is empty.');
      return;
    }

    let orderText = `Order from ${name}\nMobile: ${mobile}\nAddress: ${address}\n\nItems:\n`;
    cart.forEach(item => {
      orderText += `- ${item.name}, Qty/Weight: ${item.quantity}\n`;
    });

    // WhatsApp URL (replace with your number)
    const whatsappNumber = '8977143043';
    const whatsappURL = `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(orderText)}`;

    // Open WhatsApp Web/mobile
    window.open(whatsappURL, '_blank');

    // Reset UI and cart
    alert("Order sent to WhatsApp. Thank you!");
    clearEcommerceUI();
    showSection('home');
  }

  // Camera Handling
  let videoStream = null;
  const videoElement = document.getElementById('camera-video');
  const canvasElement = document.getElementById('camera-canvas');
  const captureBtn = document.getElementById('capture-photo');
  const retakeBtn = document.getElementById('retake-photo');
  const photoResult = document.getElementById('photo-result');

  captureBtn.addEventListener('click', capturePhoto);
  retakeBtn.addEventListener('click', retakePhoto);

  async function startCamera() {
    photoResult.innerHTML = '';
    retakeBtn.classList.add('hidden');
    captureBtn.classList.remove('hidden');
    canvasElement.classList.add('hidden');
    videoElement.classList.remove('hidden');

    try {
      videoStream = await navigator.mediaDevices.getUserMedia({ video: true });
      videoElement.srcObject = videoStream;
    } catch (error) {
      alert('Camera access denied or not available');
    }
  }

  function capturePhoto() {
    canvasElement.width = videoElement.videoWidth;
    canvasElement.height = videoElement.videoHeight;
    canvasElement.getContext('2d').drawImage(videoElement, 0, 0);
    videoElement.classList.add('hidden');
    canvasElement.classList.remove('hidden');
    captureBtn.classList.add('hidden');
    retakeBtn.classList.remove('hidden');

    // Stop video stream
    if (videoStream) {
      videoStream.getTracks().forEach(track => track.stop());
      videoStream = null;
    }

    // Show photo as base64 string
    const imageDataURL = canvasElement.toDataURL('image/png');
    photoResult.innerHTML = `<img src="${imageDataURL}" alt="Captured Image" style="width:100%; max-width: 400px; border: 1px solid #ccc; border-radius: 5px;" />`;
  }

  function retakePhoto() {
    startCamera();
  }

  // Google Maps Integration
  // Load map showing the user's location (use browser geolocation)
  window.initMap = function () {
    const mapDiv = document.getElementById('map');
    mapDiv.innerHTML = 'Loading map...';
    
    if (!navigator.geolocation) {
      mapDiv.innerHTML = 'Geolocation not supported by your browser.';
      return;
    }

    navigator.geolocation.getCurrentPosition(position => {
      const userLatLng = { lat: position.coords.latitude, lng: position.coords.longitude };
      const map = new google.maps.Map(mapDiv, { zoom: 15, center: userLatLng });
      new google.maps.Marker({ position: userLatLng, map, title: "You are here" });
    }, () => {
      mapDiv.innerHTML = 'Unable to retrieve your location.';
    });
  };

  // Initialize app
  init();
</script>

<!-- Google Maps API key is needed, place your API key below: -->
<script async defer src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=initMap"></script>

</body>
</html>
