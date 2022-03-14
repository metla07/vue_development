<template>
  <div id="showcase-app">
    <div id="show-select"
         @click="areOptionsVisible = !areOptionsVisible"
         @mouseenter="areOptionsVisible = true"
    >{{ this.selected }}
    </div>
    <div v-if="areOptionsVisible"
         class="container_select_p"
         @mouseleave="areOptionsVisible = false">
      <p class="selectP"
         v-for="(option, index) in options"
         :key="index"
         @click="selectOption(option)">{{ option.name }}
      </p>
    </div>
    <ul>
      <li class="li-container"
          v-for="(item, index) in products"
          :key="index">
        <img require :src="item.url" alt="jpeg" class="li-div-img" width="332" height="200">
        <span class="btn-delete" @click="removeProduct(item.id)"></span>
        <h3 class="h3-li">{{ item.name }}</h3>
        <p class="p-body-li">{{ item.description }}</p>
        <span class="span-group-price">{{ convertToNum(item.price) }} руб.</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['products', 'options', 'selected'],

  data() {
    return {
      areOptionsVisible: false
    }
  },
  methods: {
    convertToNum(num) {
      return num.toLocaleString().replaceAll(',', ' ')
    },
    removeProduct(id) {
      this.$emit('remove-product', id);
    },
    selectOption(option) {
      this.$emit('select-push', option)
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro&display=swap');

#showcase-app {
  overflow: scroll;
  position: absolute;
  width: 1258px;
  height: 870px;
  left: 380px;
  top: 29px;
  -ms-overflow-style: none;
  overflow-scrolling: touch;
}

#showcase-app::-webkit-scrollbar {
  width: 0;
}

ul {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-content: flex-start;
  justify-content: start;
  align-items: start;
  min-height: 1000px;
  min-width: 1058px;
  margin-top: 8px;
}

.li-container {
  z-index: 1;
  list-style: none;
  position: relative;
  margin: 1px 17px 14px 0;
  width: 332px;
  height: 423px;
  cursor: url("../assets/Vector.png"), pointer;
  background: #FFFEFB url("../assets/Rectangle 30.jpg") no-repeat;
  border-radius: 4px;
}

.li-container:hover {
  box-shadow: 1px 1px 20px lightgray;
  transition: 0.3s;
}

.li-container:hover .btn-delete {
  content: '';
  width: 32px;
  height: 32px;
  color: white;
  position: absolute;
  top: -9px;
  right: -7px;
  background: url("../assets/delete 1.png") no-repeat 8px 8px rgba(255, 132, 132, 1);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.li-container .btn-delete:hover {
  background: url("../assets/delete 1.png") no-repeat 8px 8px rgba(205, 102, 102, 90);
  transition: 0.1s;
}

.li-div-img {
  width: 332px;
  height: 200px;
  border-radius: 4px 4px 0 0;
}

.h3-li {
  position: absolute;
  width: 211px;
  height: 25px;
  left: 10px;
  bottom: 182px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
  color: #3F3F3F;
  letter-spacing: 0.01em;
}

.h3-li::first-letter {
  text-transform: uppercase;
}

.p-body-li {
  position: absolute;
  width: 300px;
  height: 80px;
  left: 2px;
  bottom: 87px;
  text-align: left;
  margin-left: 13px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 20px;
  color: #3F3F3F;
}

.span-group-price {
  position: absolute;
  width: 400px;
  height: 30px;
  left: 13px;
  bottom: 23px;
  letter-spacing: 0.02em;
  text-align: left;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;
  color: #3F3F3F;
}

/*                             select                 */

#show-select {
  position: relative;
  margin-top: 10px;
  padding-left: 16px;
  padding-bottom: 4px;
  width: 106px;
  height: 30px;
  right: -338px;
  top: -7px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  text-align: left;
  line-height: 34px;
  color: #B4B4B4;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  outline: none;
  overflow: hidden;
  background: url('../assets/Rectangle 33.png') no-repeat;
  background-position: 98px 15px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  cursor: pointer;
}

.container_select_p {
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 2px;
  right: 230px;
  z-index: 99;
  height: 106px;
  width: 123px;
  justify-content: flex-end;
  cursor: pointer;
}

.selectP {
  transition: 0.5s;
  margin-top: 4px;
  cursor: pointer;
  width: 120px;
  height: 20px;
  font-size: 12px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: normal;
  text-align: center;
  line-height: 20px;
  color: #B4B4B4;
  background: #FFFEFB;;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  outline: none;
}

.selectP:hover {
  color: black;
  background-color: rgba(255, 255, 255, 99%)
}

.selectP:active {
  color: black;
  transition: 0.1s;
  background-color: rgba(255, 255, 255, 79%)
}

</style>