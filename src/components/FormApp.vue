<template>
  <div id="form-app">
    <form action="#" method="#"
          @submit.prevent=""
          name="form"
          id="all-form">
      <label class="label-input label-1 ">Наименование товара
        <input type="text"
               id="f-ipt-name"
               name="name"
               maxlength="30"
               class="ipt-group-class"
               required
               pattern="\b^[А-Я]?[a-я],?+?[0-9-_\\.]?\b"
               placeholder="Введите наименование товара"
               oninvalid="setCustomValidity(off)"
               oninput="setCustomValidity(off)"
               v-model.trim="post.name"
               autocomplete="off"
        />
        <span>Поле является обязательным</span>
      </label>
      <label class="label-input label-4">Описание товара
        <textarea
            id="t-a-f"
            placeholder="Введите описание товара"
            maxlength="150"
            v-model="post.description">
        </textarea>
      </label>
      <label class="label-input label-2 move-input-2">Ссылка на изображение товара
        <input type="text"
               id="f-ipt-link"
               name="link"
               class="ipt-group-class"
               required
               pattern="https://.*"
               minlength="8"
               oninput="setCustomValidity(off)"
               placeholder="Введите ссылку"
               autocomplete="off"
               v-model.trim="post.url"/>
        <span>Поле является обязательным</span>
      </label>
      <label class="label-input label-3">Цена товара
        <input type="number"
               id="f-ipt-price"
               name="price"
               class="ipt-group-class"
               required
               maxlength="10"
               placeholder="Введите цену"
               v-model="post.price"
               autocomplete="off"
               pattern=/^[0-9]{1,18}$/g
               oninput="setCustomValidity(off)"
               oninvalid="setCustomValidity(off)"
        />
        <span>Поле является обязательным. Не более 18 цыфр</span>
      </label>
      <button id="btn-f"
              type="submit"
              class="form-btn"
              @click="addProduct()">Добавить товар
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: {
        price: this.price,
        id: 0,
        name: 'Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        url: "https://placeimg.com/332/200/nature/2",
        value: ''
      },
      bul: false,
    }
  },
  methods: {
    validateForm() {

      let reName = /^[А-Я]?[a-я],?\S+?[0-9-_\\.]?/.test(this.post.name);
      // console.log(reName);
      let reUrl = /^(https:[/][/]).*/.test(this.post.url);
      // console.log(reUrl);
      let rePrice = /^(\d){1,18}$/g.test(this.post.price);
      // console.log(rePrice);

      if (reName === false || this.post.name.length <= 1) {
        // console.log('name  не прошёл валидацию');
        return;
      }
      if (reUrl === false || this.post.url.length <= 5) {
           // console.log('url  не прошёл валидацию');
        return;
      }
      if (rePrice === false || this.post.price <= 0) {
        // console.log(this.bul);
        // console.log('price не прошёл валидацию');
        return;
      }

      if (reName === true && reUrl === true && rePrice === true) {
        // console.log('всё идёт отлично, валидация происходит');
        return this.bul = true;
      }
    },

    addProduct(item) {
      this.validateForm();
      if (this.bul === true) {
        item = {
          price: Math.floor(this.post.price),
          id: this.post.id,
          name: this.post.name,
          description: this.post.description,
          url: this.post.url,
          value: this.post.value
        }
        this.bul = false;
        this.$emit('add-product', item);
      } else {
        console.log('not added');
      }
    }
  }
}
</script>

<style scoped>

#form-app {
  position: absolute;
  width: 332px;
  height: 440px;
  left: 32px;
  top: 83px;
  background: #FFFEFB;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}

.label-input {
  width: 165px;
  position: relative;
  text-align: left;
  margin-left: 22px;
  padding: 1px 2px;
  top: 1px;
  height: 13px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485E;
}

.label-1 {
  top: -2px;
  right: 0.02em;
}

.label-1:after {
  content: '';
  position: absolute;
  width: 4px;
  height: 4px;
  right: 68px;
  top: 1px;
  background: #FF8484;
  border-radius: 4px;
}

span {
  position: absolute;
  width: 200px;
  height: 5px;
  right: 68px;
  bottom: -48px;
  left: 3px;
  visibility: hidden;
  font-size: 8px;
  color: #FF8484;
  font-family: 'Source Sans Pro', sans-serif;
}

.label-2 {
  top: -2px;
}

.label-2:after {
  content: '';
  position: absolute;
  width: 4px;
  height: 4px;
  right: 29px;
  top: 1px;
  background: #FF8484;
  border-radius: 4px;
}

.move-input-2 {
  margin-top: 81px;
}

.label-3 {
  top: 2px;
  left: 0;
}

.label-3:after {
  content: '';
  position: absolute;
  width: 4px;
  height: 4px;
  right: 110px;
  top: 1px;
  background: #FF8484;
  border-radius: 4px;
}

.label-4 {
  left: 0;
  top: 3px;
}

#form-app textarea {
  padding: 8px 10px 10px 16px;
  position: absolute;
  top: 14px;
  left: 1px;
  width: 258px;
  font-size: 12px;
  min-height: 90px;
  margin-top: 3px;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  resize: none;
}

#form-app textarea:focus-visible {
  outline: none;
}

#form-app textarea:hover {
  outline: 1px solid rgba(0, 0, 0, 0.1);
}

#form-app textarea::placeholder {
  width: 150px;
  height: 80px;
  position: absolute;
  top: 11px;
  left: 17px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 15px;
  text-align: left;
  color: #B4B4B4;
}

input:invalid:focus-visible {
  outline: 1px solid red;
}

input:focus-visible:invalid + span {
  visibility: visible;
}

input:valid:focus-visible {
  outline: 1px solid green;
}

input:hover {
  outline: 1px solid rgba(0, 0, 0, 0.1);
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

input[type='number'] {
  -moz-appearance: textfield;
}

/*#all-form:invalid {*/
/*  box-shadow: 0 0 5px red;*/
/*}*/

/*#all-form:valid {*/
/*  box-shadow: 0 0 1px green;*/
/*}*/

#all-form:valid .form-btn {
  background-color: #7BAE73;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.1);
  color: white;
  transition: 0.2s;
}

#all-form:valid .form-btn:active {
  background-color: darkgreen;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.1);
  color: white;
  transition: 0s;
  outline: none;
}

#all-form:valid .form-btn:focus-visible {
  outline: none;
}

#form-app .ipt-group-class {
  padding-left: 16px;
  width: 268px;
  height: 36px;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
}

#form-app .ipt-group-class::placeholder {
  height: 15px;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
}

#f-ipt-name {
  position: relative;
  top: 3px;
  left: 1px;
}

#f-ipt-name::placeholder {
  width: 170px;
  text-align: left;
  position: absolute;
  top: 11px;
  left: 15px;
}

#f-ipt-link {
  position: relative;
  top: 3px;
  left: 1px;
}

#f-ipt-link::placeholder {
  width: 85px;
  position: absolute;
  top: 11px;
  left: 15px;
}

#f-ipt-price {
  position: relative;
  top: 4px;
  left: 1px;
}

#f-ipt-price::placeholder {
  width: 70px;
  position: absolute;
  top: 10px;
  left: 15px;
}

#form-app button {
  position: relative;
  bottom: -1px;
  left: 1px;
  width: 284px;
  height: 36px;
  margin-top: 15px;
  background: #EEEEEE;
  border-radius: 10px;
  border: none;
  font-style: normal;
  font-weight: 600;
  font-size: 0.6em;
  line-height: 15px;
  text-align: center;
  letter-spacing: -0.02em;
  color: #B4B4B4;
  transition: 0.5s;
}

#form-app #all-form {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  height: 100%;
}

</style>