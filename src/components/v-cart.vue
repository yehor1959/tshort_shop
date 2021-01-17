<template>
  <div class="v-cart">
    <router-link :to="{ name: 'catalog' }" :some-value-to-pass="'Vlad'">
      <div class="v-catalog__link_to_cart">Back to Catalog</div>
    </router-link>
    <h1>Cart</h1>
    <button @click="$refs.modalName.openModal()">Open modal</button>

    <Modal ref="modalName">
      <template v-slot:header>
        <h1>Modal title</h1>
      </template>

      <template v-slot:default="slotProps">
        <p>
          {{ slotProps.srt }}  
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor incididunt ut labore et dolore magna aliqua. Nunc sed
          velit dignissim sodales ut eu sem integer vitae. Id aliquet lectus
          proin nibh nisl condimentum. Fringilla urna porttitor rhoncus dolor
          purus. Nam aliquam sem et tortor. Nisl vel pretium lectus quam id.
          Cras pulvinar mattis nunc sed. Quis ipsum suspendisse ultrices gravida
          dictum fusce ut placerat orci. Tristique magna sit amet purus.
          Fermentum et sollicitudin ac orci phasellus egestas tellus. Erat
          pellentesque adipiscing commodo elit at imperdiet dui accumsan. Felis
          eget nunc lobortis mattis aliquam faucibus. Tincidunt eget nullam non
          nisi est sit amet facilisis. Mi in nulla posuere sollicitudin aliquam
          ultrices sagittis orci. Vitae proin sagittis nisl rhoncus mattis
          rhoncus urna neque. Eget nunc scelerisque viverra mauris in aliquam
          sem fringilla ut. Nec nam aliquam sem et tortor consequat id. Commodo
          nulla facilisi nullam vehicula ipsum a. Elementum tempus egestas sed
          sed. Faucibus purus in massa tempor nec feugiat nisl pretium fusce.
        </p>
      </template>

      <template v-slot:footer>
        <div>
          <button @click="$refs.modalName.closeModal()">Cancel</button>
          <button @click="$refs.modalName.closeModal()">Save</button>
        </div>
      </template>
    </modal>

    <p v-if="!cart_data.length">There are no products in the cart...</p>
    <v-cart-item
      v-for="(item, index) in cart_data"
      :key="item.article"
      :cart_item_data="item"
      @deleteFromCart="deleteFromCart(index)"
      @increment="increment(index)"
      @decrement="decrement(index)"
    />
    <div class="v-cart__total">
      <p class="total__name">Total:</p>
      <p>{{ cartTotalCost }} grn</p>
    </div>
  </div>
</template>

<script>
import vCartItem from "./v-cart-item";
import { mapActions } from "vuex";
import Modal from './Modal'

export default {
  name: "v-cart",
  components: {
    vCartItem,
    Modal
  },
  props: {
    cart_data: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      isModalOpen: false,
    };
  },
  computed: {
    cartTotalCost() {
      let result = [];

      if (this.cart_data.length) {
        for (let item of this.cart_data) {
          result.push(item.price * item.quantity);
        }

        result = result.reduce(function (sum, el) {
          return sum + el;
        });
        return result;
      } else {
        return 0;
      }
    },
  },
  methods: {
    ...mapActions([
      "DELETE_FROM_CART",
      "INCREMENT_CART_ITEM",
      "DECREMENT_CART_ITEM",
    ]),
    increment(index) {
      this.INCREMENT_CART_ITEM(index);
    },
    decrement(index) {
      this.DECREMENT_CART_ITEM(index);
    },
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
    openModel() {
      this.isModalOpen = true;
    },
  },
};
</script>

<style>
.v-cart {
  margin-bottom: 100px;
}
.v-cart__total {
  position: fixed;
  bottom: 0;
  right: 0;
  left: 0;
  padding: 16px;
  display: flex;
  justify-content: center;
  background: #28ae68;
  color: #ffffff;
  font-size: 20px;
}
.total__name {
  margin-right: 16px;
}
</style>
