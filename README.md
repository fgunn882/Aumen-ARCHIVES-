<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AUMEN Archives</title>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family: 'Segoe UI', sans-serif;
}

body{
  background:#f5f5f5;
  color:#222;
  scroll-behavior:smooth;
}

/* HERO SECTION */
.hero{
  height:100vh;
  background:url('https://i.ibb.co/bR8R0BVV/IMG-0895.jpg') center/cover no-repeat;
  display:flex;
  justify-content:center;
  align-items:center;
  text-align:center;
  color:white;
  padding:20px;
}

.hero-content{
  background:rgba(0,0,0,0.6);
  padding:40px;
  border-radius:12px;
  max-width:500px;
}

.hero h1{
  font-size:2.7rem;
  margin-bottom:10px;
}

.hero p{
  margin-bottom:20px;
  font-size:1.1rem;
}

.btn{
  padding:12px 25px;
  background:black;
  color:white;
  border:none;
  border-radius:6px;
  cursor:pointer;
  text-decoration:none;
  font-size:1rem;
}

.btn:hover{
  background:#444;
}

/* PRODUCTS */
.products{
  padding:60px 20px;
  background:white;
}

.products h2{
  text-align:center;
  margin-bottom:40px;
  font-size:2rem;
}

.carousel{
  display:flex;
  overflow-x:auto;
  gap:20px;
  scroll-snap-type:x mandatory;
}

.carousel::-webkit-scrollbar{
  display:none;
}

.product-card{
  min-width:260px;
  background:#fafafa;
  padding:15px;
  border-radius:12px;
  box-shadow:0 4px 10px rgba(0,0,0,0.08);
  text-align:center;
  scroll-snap-align:start;
  transition:0.3s;
}

.product-card:hover{
  transform:translateY(-5px);
}

.product-card img{
  width:100%;
  border-radius:10px;
}

.product-card h3{
  margin:10px 0 5px;
}

.price{
  font-weight:bold;
  margin-bottom:10px;
}

/* CART SECTION */
.cart{
  padding:60px 20px;
}

.cart h2{
  text-align:center;
  margin-bottom:20px;
}

#cartItems{
  margin-bottom:20px;
}

input{
  width:100%;
  padding:10px;
  margin-bottom:10px;
  border:1px solid #ccc;
  border-radius:6px;
}

.total{
  font-weight:bold;
  margin-top:10px;
}

/* WHATSAPP BUTTON */
.whatsapp{
  position:fixed;
  bottom:20px;
  right:20px;
  background:#25D366;
  color:white;
  padding:15px;
  border-radius:50%;
  font-size:20px;
  text-decoration:none;
  box-shadow:0 4px 10px rgba(0,0,0,0.3);
}
</style>
</head>

<body>

<!-- HERO -->
<section class="hero">
  <div class="hero-content">
    <h1>AUMEN Archives</h1>
    <p>Fresh Finds, Best Prices</p>
    <a href="#products" class="btn">Shop Now</a>
  </div>
</section>

<!-- PRODUCTS -->
<section class="products" id="products">
  <h2>Our Collection</h2>

  <div class="carousel" id="carousel">

    <div class="product-card">
      <img src="https://i.ibb.co/ympJRRQd/7fe68f1eb866a7ab556f92d10328b942.jpg">
      <h3>Urban Classic Tee</h3>
      <p class="price">₹799</p>
      <button class="btn" onclick="addToCart('Urban Classic Tee',799)">Add to Cart</button>
    </div>

    <div class="product-card">
      <img src="https://i.ibb.co/ympJRRQd/7fe68f1eb866a7ab556f92d10328b942.jpg">
      <h3>Minimal Oversized Tee</h3>
      <p class="price">₹899</p>
      <button class="btn" onclick="addToCart('Minimal Oversized Tee',899)">Add to Cart</button>
    </div>

    <div class="product-card">
      <img src="https://i.ibb.co/ympJRRQd/7fe68f1eb866a7ab556f92d10328b942.jpg">
      <h3>Vintage Street Shirt</h3>
      <p class="price">₹999</p>
      <button class="btn" onclick="addToCart('Vintage Street Shirt',999)">Add to Cart</button>
    </div>

  </div>
</section>

<!-- CART -->
<section class="cart">
  <h2>Your Cart</h2>

  <div id="cartItems"></div>

  <input type="text" id="customerName" placeholder="Your Name">
  <input type="tel" id="customerPhone" placeholder="Your Phone Number">

  <button class="btn" onclick="placeOrder()">Place Order via Email</button>
</section>

<!-- WHATSAPP -->
<a href="https://wa.me/7990133529" target="_blank" class="whatsapp">💬</a>

<script>
let cart = [];

function addToCart(name, price){
  cart.push({name, price});
  displayCart();
}

function displayCart(){
  let cartDiv = document.getElementById("cartItems");
  cartDiv.innerHTML = "";
  let total = 0;

  cart.forEach(item=>{
    cartDiv.innerHTML += `<p>${item.name} - ₹${item.price}</p>`;
    total += item.price;
  });

  if(cart.length > 0){
    cartDiv.innerHTML += `<hr><p class="total">Total: ₹${total}</p>`;
  }
}

function placeOrder(){
  let name = document.getElementById("customerName").value;
  let phone = document.getElementById("customerPhone").value;

  if(cart.length === 0){
    alert("Cart is empty!");
    return;
  }

  if(name === "" || phone === ""){
    alert("Please fill all details!");
    return;
  }

  let items = cart.map(item => item.name + " - ₹" + item.price).join("%0D%0A");
  let total = cart.reduce((sum,item)=>sum+item.price,0);

  let subject = "New Order from AUMEN Archives";
  let body = `Customer Name: ${name}%0D%0APhone: ${phone}%0D%0A%0D%0AItems Ordered:%0D%0A${items}%0D%0A%0D%0ATotal: ₹${total}`;

  window.location.href = `mailto:omtriapthi@gmail.com?subject=${subject}&body=${body}`;
}

/* Auto Slide Carousel */
let carousel = document.getElementById("carousel");
setInterval(()=>{
  carousel.scrollBy({left:280, behavior:'smooth'});
},3000);
</script>

</body>
</html>
