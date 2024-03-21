<template>
   <h1 class="top-heading">WELCOME TO SHAWARMABS!</h1>
    <div class="container">
     <div class="categories">
      <!-- Pita Wrap -->
      <div class="category">
        <h2>Pita Wrap</h2>
        <div class="product-list">
          <div v-for="product in pitaWrapProducts" :key="product.id" class="product">
            <p>{{ product.name }} - ₱{{ product.price }}</p>
            <button @click="addToCart(product)" class="add-to-cart-btn">Add to Cart</button>
          </div>
        </div>
      </div>

      <!-- Pita Doner -->
      <div class="category">
        <h2>Pita Doner</h2>
        <div class="product-list">
          <div v-for="product in pitaDonerProducts" :key="product.id" class="product">
            <p>{{ product.name }} - ₱{{ product.price }}</p>
            <button @click="addToCart(product)" class="add-to-cart-btn">Add to Cart</button>
          </div>
        </div>
      </div>

      <!-- Doner on Rice -->
      <div class="category">
        <h2>Doner on Rice</h2>
        <div class="product-list">
          <div v-for="product in donerOnRiceProducts" :key="product.id" class="product">
            <p>{{ product.name }} - ₱{{ product.price }}</p>
            <button @click="addToCart(product)" class="add-to-cart-btn">Add to Cart</button>
          </div>
        </div>
      </div>

      <!-- Doner Platter -->
      <div class="category">
        <h2>Doner Platter</h2>
        <div class="product-list">
          <div v-for="product in donerPlatterProducts" :key="product.id" class="product">
            <p>{{ product.name }} - ₱{{ product.price }}</p>
            <button @click="addToCart(product)" class="add-to-cart-btn">Add to Cart</button>
          </div>
        </div>
      </div>
    </div>

    <!-- Shopping Cart -->
    <div class="category">
      <div class="cart">
        <h2>Your Order Summary</h2>
        <div v-if="cart.length === 0">No products added yet.</div>
        <div v-else>
          <div v-for="(item, index) in cart" :key="index" class="cart-item">
            <p>{{ item.product.name }} - ₱{{ item.product.price }} x {{ item.quantity }}</p>
            <span class="quantity">{{ item.quantity }}</span>
            <button @click="decrementQuantity(index)" class="decrement-btn">-</button>
            <button @click="incrementQuantity(index)" class="increment-btn">+</button>
            <button @click="removeFromCart(index)" class="remove-btn">Remove</button>
          </div>
          <p>Total: ₱{{ totalPrice }}</p>
        </div>
      </div>
    </div>

  </div>
</template>


<script>
export default {
  data() {
    return {
      products: [
        { id: 1, name: 'BEEF SHAWARMA', price: 89 },
        { id: 2, name: 'CHICKEN SHAWARMA', price: 89 },
        { id: 3, name: 'KEBAB WRAP', price: 89 },
        { id: 4, name: 'DONER DUO', price: 109 },
        { id: 5, name: 'TRIO MEAL', price: 169 },
        { id: 6, name: 'BEEF DONER ON RICE', price: 99 },
        { id: 7, name: 'CHICKEN DONER ON RICE', price: 99 },
        { id: 8, name: 'KEBAB DONER ON RICE', price: 99 },
        { id: 9, name: 'KEBAB and BEEF DONER PLATTER', price: 150 },
        { id: 10, name: 'KEBAB and CHICKEN DONER PLATTER', price: 150 }
      ],
      cart: []
    };
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => {
        return total + item.product.price * item.quantity;
      }, 0);
    },
    pitaWrapProducts() {
      return this.products.filter(product =>
        ['BEEF SHAWARMA', 'CHICKEN SHAWARMA', 'KEBAB WRAP'].includes(product.name.toUpperCase())
      );
    },
    pitaDonerProducts() {
      return this.products.filter(product =>
        ['DONER DUO', 'TRIO MEAL'].includes(product.name.toUpperCase())
      );
    },
    donerOnRiceProducts() {
      return this.products.filter(product =>
        ['BEEF DONER ON RICE', 'CHICKEN DONER ON RICE', 'KEBAB DONER ON RICE'].includes(product.name.toUpperCase())
      );
    },
    donerPlatterProducts() {
      return this.products.filter(product =>
        ['KEBAB AND BEEF DONER PLATTER', 'KEBAB AND CHICKEN DONER PLATTER'].includes(product.name.toUpperCase())
      );
    }
  },
  methods: {
    addToCart(product) {
      const found = this.cart.find(item => item.product.id === product.id);
      if (found) {
        found.quantity++;
      } else {
        this.cart.push({ product: product, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    incrementQuantity(index) {
      this.cart[index].quantity++;
    },
    decrementQuantity(index) {
      if (this.cart[index].quantity > 1) {
        this.cart[index].quantity--;
      }
    }
  }
};
</script>

