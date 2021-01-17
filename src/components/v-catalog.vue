<template>
  <div class="v-catalog">
    <router-link :to="{name: 'cart', params: {cart_data: CART}}" exact :click.native="cons()">
      <div class="v-catalog__link_to_cart">Cart: {{ CART.length }}</div>
    </router-link>
    <h1>Catalog</h1>
    <v-select 
      :options="categories"
      @select="sortByCategories"
      :selected="selected"
    />
    <div class="v-catalog__list">
      <v-catalog-item 
        v-for="product in filteredProducts"
        :key="product.article"  
        :product_data="product"
        @addToCart="addToCart"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from "./v-catalog-item";
import vSelect from "./v-select"
import {mapActions, mapGetters} from 'vuex';

export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
    vSelect
  },
  props: {
    someValueToPass: String
  },
  data() {
    return {
      searchText: '',
      categories: [
        {name: 'All', value: 'all'},
        {name: 'for Man', value: 'm'},
        {name: 'for Woman', value: 'w'}
      ],
      selected: 'All',
      sortedProducts: []
    };
  },
  computed: {
    ...mapGetters([
      'PRODUCTS',
      'CART'
    ]),
    filteredProducts() {
      if (this.sortedProducts.length) {
        return this.sortedProducts;
      } else {
        return this.PRODUCTS;
      }
    }
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
      'ADD_TO_CART'
    ]),
    sortByCategories(category) {
      this.sortedProducts = [];
      let vm = this;
      this.PRODUCTS.map(function(item) {
        if (item.category === category.name) {
          vm.sortedProducts.push(item);
        }
      })
      this.selected = category.name;
    },
    addToCart(data) {
      this.ADD_TO_CART(data)
    }
  },
  watch: {},
  mounted() {
    this.GET_PRODUCTS_FROM_API()
  }
};
</script>

<style>
  input {
    margin-bottom: 20px;
  }
  .v-catalog__list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }
  .v-catalog__link_to_cart {
   position: absolute;
   top: 10px;
   right: 10px;
   padding: 16px;
   border: solid 1px #aeaeae;
  }
</style>
