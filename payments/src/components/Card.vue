<script setup>
import { ref } from 'vue';

const paymentMethods = ref([
  { name: 'Wero', key: 'Wero', active: true },
  { name: 'Direct Debit', key: 'Direct Debit', active: true },
  { name: 'Creditcard', key: null, active: false, showChildren: false, children: [
    { name: 'Mastercard', key: 'Mastercard', active: true },
    { name: 'VISA', key: 'visa', active: true },
  ] },
  { name: 'bancontact', key: null, active: false, status: 'In development' },
  { name: 'iDeal', key: 'ideal', active: true, status: 'Deprecated' },
]);

const toggleChildren = (method) => {
  method.showChildren = !method.showChildren;
};
</script>

<template>
  <article class="card">
    <header class="header">
      <div class="header__textWrapper">
        <li class="header__logo"><i class="fa-regular fa-credit-card"></i></li>
        <h2 class="header__h2">Payment methods</h2>
      </div>
      <div class="header__refreshWrapper">
        <li class="header__refresh">
          <img class="header__img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/ce/Ic_refresh_48px.svg/1200px-Ic_refresh_48px.svg.png" alt="">
        </li>
      </div>
    </header>
    <div class="container">
      <div class="row">
        <div class="row__textWrapper">
          <p class="row__p"><strong>Method</strong></p>
          <p class="row__p"><strong>Key</strong></p>
        </div>
        <div class="row__activeWrapper">
          <li class="row__active"><strong>Active</strong></li>
        </div>
      </div>
      <div v-for="method in paymentMethods" :key="method.name">
        <div class="row">
          <div class="row__textWrapper">
            <p class="row__p">{{ method.name }}</p>
            <button v-if="method.children" @click="toggleChildren(method)">
              {{ method.showChildren ? 'Hide' : 'Show' }}
            </button>
            <div v-if="method.key" class="row__pWrapper">
              <p class="row__p row__p--whiteColor">{{ method.key }}</p>
            </div>
          </div>
          <div class="row__activeWrapper">
            <li v-if="method.status === 'In development'" class="row__active">
              <div class="row__devWrapper">
                <p class="row__dev">In development</p>
              </div>
            </li>
            <li v-else-if="method.status === 'Deprecated'" class="row__active">
              <div class="row__deprecatedWrapper">
                <p class="row__deprecated">Deprecated</p>
              </div>
            </li>
            <li v-else class="row__active">
              <v-switch v-model="method.active" color="blue" hide-details></v-switch>
            </li>
          </div>
        </div>
        <div v-if="method.children && method.showChildren">
          <div v-for="child in method.children" :key="child.name" class="row row--child">
            <div class="row__textWrapper">
              <p class="row__p">{{ child.name }}</p>
              <div v-if="child.key" class="row__pWrapper">
                <p class="row__p row__p--whiteColor">{{ child.key }}</p>
              </div>
            </div>
            <div class="row__activeWrapper">
              <li class="row__active">
                <v-switch v-model="child.active" color="blue" hide-details></v-switch>
              </li>
            </div>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>

<style scoped>
.card {
  width: 100%;
  height: 100%;
  background-color: #fff;
  display: block;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.row__textWrapper {
  gap: 5rem;
}

.row__active {
  display: flex;
  align-items: center;
}

.row__textWrapper {
  display: flex;
  align-items: center;
}

.row__p--whiteColor {
  color: #fff;
}

.row__pWrapper {
  background: grey;
  width: 160px;
  height: 29px;
  align-items: center;
  display: flex;
  border-radius: 0.7rem;
  justify-content: center;
}

.header {
  display: flex;
  gap: 1rem;
  align-items: center;
  padding: 0.4rem;
  justify-content: space-between;
}

.header__textWrapper {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.header__logo {
  list-style: none;
}

.header__refresh {
  list-style: none;
}

.header__refreshWrapper {
  width: 40px;
  height: 40px;
  align-items: center;
  padding: 0.5rem;
  display: flex;
  justify-content: center;
  background: #40A2E3;
  transition: 0.3s all;
  border-radius: 0.5rem;
}

.header__img {
  height: 100%;
  width: 100%;
}

.header__refreshWrapper:hover {
  cursor: pointer;
  width: 45px;
  height: 45px;
}

.container {
  width: 100%;
  height: 100%;
  border: black solid 1px;
  padding-bottom: 200px;
}

.row__devWrapper {
  background: #7BC9FF;
  width: 160px;
  height: 29px;
  align-items: center;
  display: flex;
  border-radius: 0.7rem;
  justify-content: center;
  color: #fff;
}

.row__deprecatedWrapper {
  background: #FF7F3E;
  width: 160px;
  height: 29px;
  align-items: center;
  display: flex;
  border-radius: 0.7rem;
  justify-content: center;
  color: #fff;
}

.row {
  display: flex;
  gap: 5rem;
  align-items: center;
  border-bottom: black solid 1px;
  justify-content: space-between;
  padding-left: 1rem;
}

.row__p {
  padding-left: 0.5rem;
}

.row__activeWrapper {
  padding-left: 27rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.row__active {
  list-style: none;
  padding-right: 1rem;
}

.row--child {
  padding-left: 2rem;
}
</style>
