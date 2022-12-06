<script>
import { registerRuntimeHelpers } from "@vue/compiler-core";
import ITEMS from "./assets/API.json";

export default {
  data() {
    return {
      title: "My new ecommerce",
      items: ITEMS,
    };
  },

  computed: {
    selectedItems() {
      return this.items.slice(0, 5);
    },
    totalCartItems() {
      let contador = 0;
      for (let index = 0; index < this.items.length; ++index) {
        contador += this.items[index].quantity;
      }
      return contador;
      // //       const contador= null;
      // // const totalItems= selectedItems.quantity;
      // // totalItems.reduce((acumulator,before){
      // //   return acumulator + before;
      // // console.log(totalItems);
      // // },0);
    },
    subTotalPrice() {
      let contador2 = 0;
      for (let index = 0; index < this.items.length; ++index) {
        contador2 += this.items[index].price * this.items[index].quantity;
      }
      return contador2;
    },
    cartlimit(){
      return this.items.lenght >= 5;
    }

    // subTotal(){
    //   // let total=0;
    //   // let apiPrice= this.items.quantity;
    //   // let apiQuantity= this.items.price;
    //   // this.apiPrice.forEach((item, i)=>{
    //   //   total += apiQuantity*apiPrice;
    //   // });
    //   // return total;
    // //   for (let index=0; index<this.items.quantity; i++){
    // //   return sum+= this.items.quantity[index];
    // // }
    // },
  },
};
</script>

<template>
  <header>
    <nav class="flex">
      <p class="text-sky-700 text-lg">{{ title }}</p>
      <div>TOTAL NUMBERS OF ITEMS IN THE CART IS   {{ totalCartItems }}</div>
    </nav>
  </header>
  <section>
    <table>
      <thead class="font-extrabold">
        <tr>
          <th>Name</th>
          <th>Photo</th>
          <th>Price</th>
          <th>Quantity</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody v-for="item of selectedItems" :key="item.uuid">
        <tr>
          <td>{{ item.name }}</td>
          <td class="w-10 h-10 bg-teal-600">photo</td>
          <!-- <img class="w-0.01" :src="item.image" :alt="items.name">  -->
          <td>{{ item.price }} €</td>
          <td>
            <input type="number" v-model="item.quantity" placeholder="0" />
          </td>
          <td>{{ item.price * item.quantity }} €</td>
        </tr>
      </tbody>
    </table>
    
    <div>Subtotal Price: {{ subTotalPrice }} € </div>
    <div>
      <button v-if="cartlimit">Confirm your purchase</button>
      <p v-else>If you buy at least 5 products, you get free shipping!</p>
     
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Nunito:400,700&display=swap');
*{
  font-family:Verdana, Geneva, Tahoma, sans-serif
}
</style>
