<template>
  <div class="container">
    
    <div class="wrapper">
      <header class="menu">
        <h1 class="menu__title">GBPUSD </h1>
      </header>
      <div class="card-list"> 
        <h3 class="card-title">M1</h3>
        <CardItems :ordersTF="ordersTF('GBPUSD',1)"/>
        <h3 class="card-title">M5</h3>
        <CardItems :ordersTF="ordersTF('GBPUSD',5)"/>
        <h3 class="card-title">M15</h3>
        <CardItems :ordersTF="ordersTF('GBPUSD',15)"/>
        <h3 class="card-title">H1</h3>
        <CardItems :ordersTF="ordersTF('GBPUSD',60)"/>
      </div>
           
    </div>

    <div class="wrapper">
      <header class="menu">
        <h1 class="menu__title">EURUSD</h1>
      </header>
      <div class="card-list"> 
        <h3 class="card-title">M1</h3>
        <CardItems :ordersTF="ordersTF('EURUSD',1)"/>
        <h3 class="card-title">M5</h3>
        <CardItems :ordersTF="ordersTF('EURUSD',5)"/>
        <h3 class="card-title">M15</h3>
        <CardItems :ordersTF="ordersTF('EURUSD',15)"/>
        <h3 class="card-title">H1</h3>
        <CardItems :ordersTF="ordersTF('EURUSD',60)"/>
      </div>          
    </div>

  </div>
</template>
<script>
import CardItems from './CardItems'
export default {
  name: 'Card',
  components: {CardItems},
  props: ['orders'],
  mounted() {
    //console.log(this.orders)
  },
  methods: {
    ordersTF: function(symbol,mN) {
      return this.orders
        .filter(f => f.symbol === symbol)
        .filter(m => m.magicNumber === mN)
    }
  }
}
</script>


<style>
/*@import url("https://fonts.googleapis.com/css?family=Lato:300,400");*/
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

html, body {
  width: 100%;
  height: 100%;
}

body {
  font-family: "Lato", sans-serif;
  background-color: #e5eef9;
  display: flex;
  align-items: space-evenly;
  flex-direction: column;
}

.container {
  display: flex;
  justify-content: space-evenly;
}

.wrapper {
  background-color: #fff;
  width: 285px;
  height: 100%;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  box-shadow: 0 10px 25px #dcdcdc;
  margin-bottom: 25px;
}

.menu {
  width: 100%;
  height: 7.5%;
  border-radius: 10px 10px 0px 0px;
  display: flex;
  justify-content: center;
}
.menu__icon {
  width: 17.5px;
  height: 50%;
  margin: 0 10px;
  align-self: flex-end;
}
.menu__title {
  font-size: 18px;
  align-self: flex-end;
  color: #43639d;
  margin-bottom: 2px;
  text-align: center;
}

.list {
  display: flex;
  list-style: none;
  justify-content: flex-start;
  margin-bottom: 10px;
  flex-wrap: wrap;
}

.list-item {
  width: 15px;
  height: 15px;
  margin: 4px 4px;
  background-color: white;
  color: bisque;
  text-align: center;
  font-size:14px;

  /*border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  
  border-bottom: 5px solid green;*/
  /*border: 2px solid green;*/
  
}


.list-item-lost {
  background-color: red;
}

.list-item-win {
  background-color: green;
}

.card-list {
  width: 100%;
  overflow-y: hidden;
  padding: 20px 0 0;
  flex-grow: 1;
}

.card-title {
  width: 100%;
  text-align: center;
  margin-bottom: 5px;
}

.card {
  width: 90%;
  margin: 0 auto;
  margin-bottom: 12.5px;
  border-radius: 5px;
  padding: 15px 25px;
  box-shadow: 0 10px 25px #dcdcdc;
}
.card__number {
  text-align: center;
  color: #fff;
  margin-bottom: 10px;
}
.card__owner {
  color: #fff;
  font-size: 13px;
  font-weight: 300;
  margin-bottom: 5px;
}
.card__info {
  display: flex;
}
.card__amount {
  margin-left: 10px;
}
.card__integral, .card__amount {
  font-size: 10.5px;
  color: #fff;
  font-weight: 300;
  letter-spacing: 0.25px;
}
.card--one {
  background: linear-gradient(to right, #d194ff, #9389ff);
}
.card--two {
  background: linear-gradient(to right, #7cbfee, #00d0b8);
}
.card--three {
  background: linear-gradient(to right, #ff77a7, #ff7b7e);
}

.author {
  text-decoration: none;
  font-size: 12.5px;
}
.author:link, .author:visited, .author:hover, .author:active {
  color: #43639d;
}

</style>
