<template>
<body>

  <select class="filter">
    <option>по возрастанию цен</option>
    <option>по убыванию цен</option>
    <option>по наименованию</option>
  </select>

  <div class="error">
    <p v-if="errors.length">
    <b>Пожалуйста исправьте указанные ошибки:</b>
    <ul>
      <li v-for="error in errors"
      :key="error.id">{{ error }}</li>
    </ul>
    </p>
  </div>
  
  <div class="form">

    <p class="h-add-product">Добавление товара</p>

    <p class="h-name-product required"> Наименование товара </p>
    <input v-model="name" 
    class="nameproduct" placeholder="Введите наименование товара"
    name="name" for="name"/>

    <p class="h-product-description">Введите описание товара</p>
    <textarea v-model.trim="products.text" class="product-description" placeholder="Введите описание товара"/>

    <p class="h-enter-link required">Ссылка на изображение товара</p>
    <input v-model="img" class="enter-link" placeholder="Введите ссылку"
    name="img" for="img"/>

    
    <p class="h-price-product required" required="required">Цена товара</p>
    <input v-model="cena" class="price-product" placeholder="Введите цену"
    name="cena" for="cena" type="number"/>

    <button @click="addProduct" class="add-button"
    :class="{ active: addButtonActive }">Добавить товар</button>

  </div>
    
  <div class="list">

    <ul class="products clearfix">

      <li class="product-wrapper"
      v-for="product in products"
        :key="product.id">
        <a href="" class="product">
          <div class="product-photo">
            <button @click="removeProduct(product)"></button>
            <img :src="product.img" alt="">
          </div>
          <p class="h-description"> {{ product.name }} </p>
          <b class="description"> {{ product.text }} </b>
      <b class="cena"> {{ product.cena }} ₽ </b>
        </a>
      </li>

    </ul>
    
  </div>

  
</body>
</template>

<script>
export default {
  name: 'DefaultLayout',
  props: {
    msg: String
  },
  data() {
    return {
      products:[
        {
        id: "1",
        name: "Кружка",
        img: "https://avatars.mds.yandex.net/get-mpic/5266697/img_id1186982211701183156.png/orig",
        text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        cena: "5 000",
        basket: false
      },
       {
        id: "2",
        name: "Велик",
        img: "https://st.depositphotos.com/1003369/3697/i/450/depositphotos_36975627-stock-photo-mountain-bicycle-bike-on-white.jpg",
        text: "Довольно-таки интересное описание товара в несколько строк",
        cena: "15 000",
        basket: false
      }
      ],
      newProduct:"",
      errors: [],
      name: null,
      img: null,
      cena: null,
      addButtonActive: false
    }
  },
  methods: {
    createNewId() {
      let maxId = Math.max(...this.products.map(i => i.id)); //Определяет максимальный id в массиве
      let newId = (maxId > 0) ? maxId+1 : 1 //Добавляет 1 к максимальному id, если же массив пуст, выводит 1
      return(newId);
    },
    addProduct: function () {
      if (this.name && this.img && this.cena) {
        this.products.push({
          id: this.createNewId(),
          name: this.name,
          img: this.img,
          text: this.products.text,
          cena: this.cena,
          basket: false
        });
      }

      this.errors = [];

      if (!this.name) {
        this.errors.push('Требуется указать имя.');
      }
      if (!this.img) {
        this.errors.push('Требуется указать ссылку.');
      }
      if (!this.cena) {
        this.errors.push('Требуется указать цену.');
      }
      this.name = ""
      this.img = ""
      this.products.text = ""
      this.cena = ""
    },
    removeProduct: function(product) {
      this.products.splice(this.products.indexOf(product), 1);
    }
    
  }

  

}
</script>


<style>

body {
  size: 100%;
  background: #E5E5E5;
  background-size: 100%;
}

.h-add-product {
/* Добавление товара */
position: absolute;
left: 10px;
top: -75px;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 600;
font-size: 28px;
line-height: 35px;

color: #3F3F3F;
}
/*-22 -97 */
.h-name-product {
/* Наименование товара */
position: absolute;
width: 100px;
height: 13px;
left: 20px;
top: 0px;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 400;
font-size: 10px;
line-height: 13px;
/* identical to box height */

letter-spacing: -0.02em;

/* Temp / Darks / Lesser */

color: #49485E;
}

.nameproduct {
/* Rectangle 28 */
position: absolute;
width: 284px;
height: 36px;
left: 20px;
top: 27px;
/* Darks & Whites / White */
background: #FFFEFB;
box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
border-radius: 4px;
}

.h-product-description {
/* Описание товара */
position: absolute;
width: 105px;
height: 13px;
left: 20px;
top: 69px;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 400;
font-size: 10px;
line-height: 13px;
/* identical to box height */
letter-spacing: -0.02em;
/* Temp / Darks / Lesser */
color: #49485E;
}

.h-enter-link {
/*Ссылка на изображение товара */
position: absolute;
width: 134px;
height: 13px;
left: 20px;
top: 210px;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 400;
font-size: 10px;
line-height: 13px;
/* identical to box height */
letter-spacing: -0.02em;
/* Temp / Darks / Lesser */
color: #49485E;
}

.enter-link {
/* Rectangle 28 */
position: absolute;
width: 284px;
height: 36px;
left: 20px;
top: 237px;
/* Darks & Whites / White */
background: #FFFEFB;
box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
border-radius: 4px;
}

.h-price-product {
/* Цена товара */
position: absolute;
width: 59px;
height: 13px;
left: 20px;
top: 279px;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 400;
font-size: 10px;
line-height: 13px;
/* identical to box height */
letter-spacing: -0.02em;
/* Temp / Darks / Lesser */
color: #49485E;
}

.price-product {
/* Rectangle 28 */
position: absolute;
width: 284px;
height: 36px;
left: 20px;
top: 306px;
/* Darks & Whites / White */
background: #FFFEFB;
box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
border-radius: 4px;
}

.product-description {
/* Rectangle 28 */
position: absolute;
width: 284px;
height: 108px;
left: 20px;
top: 96px;
/* Darks & Whites / White */
background: #FFFEFB;
box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
border-radius: 4px;
resize: none;
}

.add-button {
/* Rectangle 29 */
position: absolute;
width: 284px;
height: 36px;
left: 24px;
top: 366px;

background: #EEEEEE;
border-radius: 10px;
}

.add-button.active {
position: absolute;
width: 284px;
height: 36px;
left: 24px;
top: 366px;

background: #7BAE73;
box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
border-radius: 10px;
}

.list {
  position: absolute;
  left: 380px;
  top: 75px;
  display: grid;
  grid-gap: 5px;
  grid-template-columns: repeat(auto-fit, 1432px);
  grid-template-rows: repeat(2, 332px);
}

.filter {
/* Rectangle 28 */
position: absolute;
width: 121.49px;
height: 36px;
left: 1287px;
top: 31px;
/* Darks & Whites / White */
background: #FFFEFB;
box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
border-radius: 4px;
}

/* Rectangle 1 */
.form {
position: absolute;
width: 332px;
height: 440px;
left: 32px;
top: 83px;

background: #FFFEFB;
box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
border-radius: 4px;
}

.product-block {
position: sticky;
width: 332px;
height: 423px;
left: 380px;
top: 83px;

background: #FFFEFB;
box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
border-radius: 4px;
}

.product-img {
/* Rectangle 31 */
width: 100%;
padding: 100px;
font-size: inherit;

background: url("https://pola-store.ru/32-7228-large/polaroid-supercolor.jpg");
border-radius: 4px 4px 0px 0px;
}

.h-description {
position: absolute;
width: 100px;
height: 25px;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 600;
font-size: 20px;
line-height: 25px;

color: #3F3F3F;
}

.description {
position: absolute;
width: 322px;
height: 60px;
left: 5px;
top: 270px;

font-size: inherit;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 550;

line-height: 20px;

color: #3F3F3F;
}

.cena {
position: absolute;
width: 117px;
height: 30px;
left: 20px;
top: 370px;

font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 600;
font-size: 24px;
line-height: 30px;

color: #3F3F3F;
}

p.required:after
{
  color: red;
  content: " *";
}

.error {
position: absolute;
background-color: #eee;
box-sizing: content-box;
border-radius: 8px;
top: 550px;
border: 10px solid rgba(255, 255, 255, 0);

color: #fc2d2d;
}

/*/////////////////////////////*/

.product-wrapper {
	display: block;
	width: 100%;
	float: left;
	transition: width .2s;
}

@media only screen and (min-width: 450px) {
	.list {
		width: 50%;
	}
}

@media only screen and (min-width: 768px) {
	.list {
		width: 33.333%;
	}
}

@media only screen and (min-width: 1000px) {
	.product-wrapper {
		width: 25%;
	}
}

.product {
	display: block;
	border-radius: 4px;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
	position: relative;
	background: #FFFEFB;
	margin: 0 20px 20px 0;
	text-decoration: none;
	color: #474747;
	z-index: 0;
  width: 332px;
	height: 423px;
}

.products {
	list-style: none;
	margin: 10px -10px 10px 10px;
	padding: 0;
}


/*photo */

.product-photo {
	position: relative;
	padding-bottom: 70%;
	overflow: hidden;
}

.product-photo img {
	position: absolute;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	max-width: 100%;
	max-height: 90%;
	margin: auto;
	transition: transform .4s ease-out;
}

.product:hover .product-photo img {
	transform: scale(1.05);
}

/* Описание */

.product p {
	position: relative;
	margin: 0;
	font-size: 1em;
	line-height: 1.4em;
	height: 5.6em;
	overflow: hidden;
}

.product p:after {
	content: '';
	display: inline-block;
	position: absolute;
	bottom: 0;
	right: 0;
	width: 4.2em;
	height: 1.6em;
	background: linear-gradient(to left top, #fff, rgba(255, 255, 255, 0));
}

/* Всплывающие кнопки */


.product:hover .product-preview {
	transform: translateY(0);
	opacity: 1;
}

.product-buttons-wrap {
	position: absolute;
	top: 0;
	left: -1px;
	right: -1px;
	bottom: 0;
	visibility: hidden;
	opacity: 0;
	transform: scaleY(.8);
	transform-origin: top;
	transition: transform .2s ease-out;
	z-index: -1;
	backface-visibility: hidden;
}

.product-buttons-wrap:before {
	content: "";
	float: left;
	height: 100%;
	width: 100%;
}

.buttons {
	position: relative;
	top: -1px;
	padding: 20px;
	background: #fff;
	box-shadow: 0 0 20px rgba(0, 0, 0, .5);
	border: 1px solid #56bd4b;
	border-radius: 3px;
}

</style>
