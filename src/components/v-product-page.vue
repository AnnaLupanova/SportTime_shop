<template>
<div class="v-product-page">
  <v-header/>
  <div class="page">
    <img v-if="product.image" class="v-catalog-item__img" :src="require('../images/' + product.image)" alt="img">
    <div class="product">
      <p style="font:700 20px 'Montserrat', sans-serif;">{{this.product.name}}</p>
      <p style="font:500 16px 'Montserrat', sans-serif;">Article:{{this.product.article}}</p>
      <p style="font:500 16px 'Montserrat', sans-serif;"> <span class="desc">Description: </span>{{this.product.description}}</p>
      <p style="font:500 16px 'Montserrat', sans-serif;"><span class="desc">Price:</span> {{this.product.price}}</p>
      <button class="btn" @click="addToCart">Buy</button>
    </div>
  </div>
  <v-footer/>
</div>
</template>

<script>
import {mapGetters, mapActions} from 'vuex'
import vHeader from './v-header'
import vFooter from './v-footer'
import axios from 'axios'
export default {
name: "v-product-page",
  components:{
  vHeader,vFooter
  },
  props:{

  },
  computed:{
  ...mapGetters([
      'PRODUCTS','PRODUCTS_RUNNING','PRODUCTS_FITNESS','PRODUCTS_FOOTBALL'
  ]),
    product(){
    let result = {};
    let vm =this;
    this.PRODUCTS.map(function (item){
      if (item.article === vm.$route.query.product){
        result = item;
      }
    })
      return result;
    }

  },
  methods:{
  ...mapActions([
      'GET_PRODUCTS_FROM_API'
  ]),
    addToCart() {

      axios.post('http://localhost:8080/basket', {
        article: this.product.article
      })
          .then(function (response) {
            console.log(response);

          })
          .catch(function (error) {
            console.log(error);
          });

    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
  }
}
</script>

<style>
@import '../assets/style/style.scss';
.desc{
  font:700 20px 'Montserrat', sans-serif;
}
.btn {
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
.btn:hover {
  background: #2EE59D;
  box-shadow: 0 15px 20px rgba(46,229,157,.4);
  color: white;
  transform: translateY(-7px);
}
.page{
  display: flex;
  margin: 30px 150px;

}
.product{
  text-align: left;
  margin-left: 20px;
}
</style>