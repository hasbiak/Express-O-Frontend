<template>
  <div class="home">
    <b-container class="centered">
      <img alt="Vue logo" src="../assets/logo.png" />
      <Navbar />
      <b-card>
        <h5>Interpolation</h5>
        <p>My Name is {{ name }}</p>
      </b-card>
      <b-card>
        <h5>Computed</h5>
        <p>Original Message : {{ message }}</p>
        <p>Reverse Message : {{ reverseMessage }}</p>
      </b-card>
      <b-card>
        <h5>Directive</h5>
        <hr />
        <h6>v-if</h6>
        <div v-if="rule === 1">Kamu Adalah Admin</div>
        <div v-else-if="rule === 2">Kamu Adalah Kasir</div>
        <div v-else>Kamu Adalah User</div>
        <hr />
        <h6>v-show</h6>
        <div v-show="rule === 3">Kamu Bukan Siapa Siapa</div>
        <hr />
        <h6>v-for</h6>
        <ul>
          <li v-for="(item, index) in dataProduct" :key="index">
            {{ index }}
            <h5>{{ item.product_name }}</h5>
            <p>{{ item.product_price }}</p>
          </li>
        </ul>
        <hr />
        <h6>v-on & v-model</h6>

        <hr />
        <h6>v-on</h6>
        <button v-on:click="boom()">Click Me !</button>
        <input type="text" v-model="searchData" v-on:keyup.enter="search()" />
        <hr />
        <h6>v-bind</h6>
        <a v-bind:href="rule === 1 ? urlGoogle : urlYoutube">Click Here</a>
      </b-card>
      <b-card>
        <h5>Component Comunication</h5>
        <!-- <FormInput
          v-bind:dataProductName="product_name"
          @changeProductName="product_name = $event"
        /> -->
        <FormInput
          v-bind:dataProductName="product_name"
          @changeProductName="product_name = $event"
        />
        <br />
        <label>{{ product_name }}</label>
      </b-card>
    </b-container>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '../components/_base/Navbar'
import FormInput from '../components/_base/FormInput'
export default {
  name: 'Home',
  components: {
    Navbar,
    FormInput
  },
  data() {
    return {
      name: 'Hasbi Alwi Kusmana',
      message: 'Hello World',
      rule: 1,
      searchData: '',
      dataProduct: [
        { product_name: 'Meja', product_price: '50000' },
        { product_name: 'Kursi', product_price: '50000' }
      ],
      urlGoogle: 'http://google.com',
      urlYoutube: 'http://youtube.com',
      product_name: 'Sepatu Baru'
    }
  },
  computed: {
    reverseMessage: function() {
      return this.message
        .split(' ')
        .reverse()
        .join(' ')
    }
  },
  methods: {
    boom() {
      console.log('Boom !')
      alert('Boom !')
    },
    search() {
      console.log('Proses Search !')
      console.log(this.searchData)
    },
    changeProductName(event) {
      this.product_name = event
    }
  }
}
</script>

<style scoped>
.centered {
  text-align: center;
}
</style>
