<template>
  <div id="app">
    <HeaderApp/>
    <FormApp @add-product="addProduct" />
    <ShowcaseApp :products="products"
                 :options="options"
                 :selected="selected"
                 @select-push="selectOption"
                 @remove-product="removeProduct"
    />
  </div>
</template>

<script>
import HeaderApp from './components/HeaderApp.vue'
import ShowcaseApp from "@/components/ShowcaseApp";
import FormApp from "@/components/FormApp";
import Products from './products.json';


export default {
  name: 'app',

  data() {
    return {
      products: Products,
      selected: 'По умолчанию',
      counter: 0,
      options: [
        {name: 'По умолчанию', value: 'byOll'},
        {name: 'Min price', value: 'min'},
        {name: "Max price", value: 'max'}
      ]
    }
  },
  mounted() {
    if (localStorage.products) {
      this.products = JSON.parse(localStorage.products);
    }
  },
  components: {
    FormApp,
    ShowcaseApp,
    HeaderApp
  },
  methods: {
    removeProduct(id) {
      this.products = this.products.filter(product => product.id !== id);
      localStorage.products = JSON.stringify(this.products);
    },
    addProduct(item) {
      if (this.counter === 0) {
        this.products.forEach(element => element.id = this.counter++);
        item.id = this.counter++
        this.products.push(item);
        localStorage.products = JSON.stringify(this.products);
      } else {
        item.id = this.counter++
        this.products.push(item);
        localStorage.products = JSON.stringify(this.products);
      }
    },
    selectOption(option) {
      this.selected = option.name;
      switch (option.value) {
        case 'byOll':
          this.products = this.products.sort((a, b) => a.id - b.id);
          break;
        case 'max':
          this.products = this.products.sort((a, b) => b.price - a.price);
          break;
        case 'min':
          this.products = this.products.sort((a, b) => a.price - b.price);
          break;
        default:
          break;
      }
      localStorage.products = JSON.stringify(this.products);
    }
  }
}
</script>

<style>

* {
  margin: 0 auto;
  padding: 0;
}

html {
  background: #E5E5E5;
  width: 100%;
}
body {
  max-width: 1440px;
  margin: 0 auto;
}
@media screen and (max-width: 1440px){
  html {
    transform: scale(0.913);
    position: absolute;
    top: -45px;
    left: -72px;
  }
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  overflow: hidden;
  position: relative;
  width: 1440px;
  height: 900px;
  background: rgba(255, 254, 251, 0.8);
}
</style>
