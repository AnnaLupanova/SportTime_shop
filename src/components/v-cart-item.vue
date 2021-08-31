<template>
  <div class="v-cart-item">
    <img class="v-cart-item__img" v-if="cart_item_data.image" :src="require('../images/' + cart_item_data.image)" alt="">
    <div class="v-cart-item__info">
      <p>{{this.cart_item_data.name}}</p>
      <p>{{this.cart_item_data.price}}</p>
      <p>{{this.cart_item_data.article}}</p>
    </div>
    <div class="cart_item_data__quantity">
      <p>Quantity: </p>
        <span class="quantity_btn" @click="decrement">-</span>
      {{this.cart_item_data.quantity}}
      <span class="quantity_btn" @click="increment">+</span>
    </div>
    <button @click="deleteFromCart">Delete</button>
  </div>
</template>

<script>


export default {
name: "v-cart-item",
  props:{
  cart_item_data:{
    type:Object,
    default(){
      return[]
    }
  }
  },
  methods:{

  decrement(){
    this.$emit('decrement')
  },
    increment(){
      this.$emit('increment')
    },

    deleteFromCart(){
      this.$emit('deleteFromCart')
    }

  },



}
</script>

<style lang="scss">
@import '../assets/style/style.scss';
.v-cart-item{
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-between;
align-items: center;
  box-shadow: 0 0 8px 0 #e0e0e0;
  padding: $padding*2;
  margin: 0 100px 16px 100px;
  &__img{
    width: 200px;
  }
 .quantity_btn{
   cursor: pointer;
 }
  button{
    text-decoration: none;
    outline: none;
    display: inline-block;
    margin: 5px 66px 0px;
    padding: 10px 17px;
    border-radius: 45px;
    border: none;
    font-family: 'Montserrat', sans-serif;
    font-size: 11px;
    text-transform: uppercase;
    text-align: center;
    letter-spacing: 3px;
    font-weight: 600;
    color: #524f4e;
    background: white;
    box-shadow: 0 8px 15px rgba(0,0,0,.1);
    transition: .3s;
  }
  button :hover {
    background: #2EE59D;
    box-shadow: 0 15px 20px rgba(46,229,157,.4);
    color: white;
    cursor: pointer;
    transform: translateY(-7px);
  }
}

</style>