<template>
  <div class="Product">
    <b-container class="bv-example-row">
      <b-row>
        <b-col class="logo">
          <img alt="" src="../assets/img/coffe.png" />
          <a href="">Express-O Coffee</a>
        </b-col>
        <b-col class="menu">
          <Navbar />
        </b-col>
        <b-col class="user-menu">
          <ul>
            <li><img src="../assets/img/search.png" /></li>
            <li><img src="../assets/img/chat.png" /></li>
            <li>
              <a href=""><img src="../assets/img/profile.png"/></a>
            </li>
          </ul>
        </b-col>
      </b-row>
    </b-container>
    <!-- <Header /> -->
    <hr />
    <b-container class="bv-example-row">
      <b-row>
        <b-col cols="4">
          <h4>Promo for you</h4>
          <p>Coupon will be updated every weeks.<br />Check them out!</p>
          <div id="Promo-content"></div>
          <div id="box1"></div>
          <div id="box2"></div>
          <div id="box3"></div>
          <img src="../assets/img/beefspaghetti.png" />
          <h2>Beef Spaghetti<br />20% OFF</h2>
          <h3>Buy 1 Choco Oreo and get 20% off for<br />Beef Spaghetti</h3>
          <div class="dashln"></div>
          <div class="cc">COUPON CODE</div>
          <div class="code">FNPR15RG</div>
          <div class="valid">Valid until October 10th 2020</div>
          <a class="btn btn-primary btn-lg" href="#" role="button">
            Apply Coupon
          </a>
          <div class="term">
            <p>Term and conditions</p>
          </div>
          <ol>
            <li>You can only apply 1 coupon per day</li>
            <li>It only for dine in</li>
            <li>Buy 1 get 1 only for new user</li>
            <li>Should make member card to apply coupon</li>
          </ol>
        </b-col>
        <b-col cols="8">
          <div class="category">
            <ul>
              <li><a href="">Favorite Product</a></li>
              <li><a href="">Coffee</a></li>
              <li><a href="">Non Coffee</a></li>
              <li><a href="">Foods</a></li>
              <li><a href="">Add-on</a></li>
            </ul>
          </div>
          <b-row>
            <b-col
              xl="3"
              lg="4"
              md="6"
              sm="12"
              v-for="(item, index) in products"
              :key="index"
            >
              <b-card
                :title="item.product_name"
                img-src="https://www.averiecooks.com/wp-content/uploads/2017/11/caramelmacchiato-18.jpg"
                img-alt="Image"
                img-top
                tag="article"
                style="max-width: 20rem;"
                class="mb-2"
              >
                <b-card-text> Rp. {{ item.product_price }} </b-card-text>

                <b-button variant="primary">Add to Cart</b-button>
                <b-button variant="success" @click="setProduct(item)"
                  >Update</b-button
                >
                <b-button
                  variant="danger"
                  @click="deleteProduct(item.product_id)"
                  >Delete</b-button
                >
              </b-card>
            </b-col>
          </b-row>
          <b-pagination
            v-model="currentPage"
            :total-rows="rows"
            :per-page="limit"
            @change="handlePageChange"
          ></b-pagination>
        </b-col>
      </b-row>
    </b-container>
    <hr />
    <!-- <Footer /> -->
    <b-container class="bv-example-row">
      <b-row>
        <b-col class="desc">
          <div class="logo">
            <img src="../assets/img/coffe.png" />
            <a href="">Express-O Coffee</a>
          </div>
          <p>
            Coffee Shop is a store that sells some good<br />meals, and
            especially coffee. We provide<br />high quality beans
          </p>
          <div class="social-media">
            <img src="../assets/img/facebook.png" />
            <img src="../assets/img/twitter.png" />
            <img src="../assets/img/instagram.png" />
          </div>
          <div class="copyright">
            <p>&copy;2020CoffeeStore</p>
          </div>
        </b-col>
        <b-col class="product">
          <h4>Product</h4>
          <ul>
            <li><a href="">Dashboard</a></li>
            <li><a href="">Pricing</a></li>
            <li><a href="">Locations</a></li>
            <li><a href="">Countries</a></li>
            <li><a href="">BLog</a></li>
          </ul>
        </b-col>
        <b-col class="engage">
          <h4>Engage</h4>
          <ul>
            <li><a href="">Coffee Shop ?</a></li>
            <li><a href="">FAQ</a></li>
            <li><a href="">About Us</a></li>
            <li><a href="">Privacy Policy</a></li>
            <li><a href="">Term of Service</a></li>
          </ul>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Navbar from '../components/_base/Navbar'
import axios from 'axios'
export default {
  name: 'Product',
  components: {
    Navbar
  },
  data() {
    return {
      products: [],
      alert: false,
      isMsg: '',
      product_id: '',
      currentPage: 1,
      totalRows: null,
      limit: 12,
      page: 1
    }
  },
  created() {
    this.getProduct()
  },
  methods: {
    getProduct() {
      axios
        .get(
          `${process.env.VUE_APP_URL}/product?page=${this.page}&limit=${this.limit}`
        )
        .then(response => {
          console.log(response)
          this.totalRows = response.data.pagination.totalData
          this.products = response.data.data
        })
        .catch(error => {
          console.log(error)
        })
    },
    postProduct() {
      console.log(this.form)
      axios
        .post(`${process.env.VUE_APP_URL}/product`, this.form)
        .then(response => {
          console.log(response)
          this.alert = true
          this.isMsg = response.data.msg
          this.getProduct()
        })
        .catch(error => {
          console.log(error.response)
        })
    },
    setProduct(data) {
      console.log(data)
      this.form = data
      this.product_id = data.product_id
    },
    patchProduct() {
      console.log(this.form)
      axios
        .patch(
          `${process.env.VUE_APP_URL}/product/${this.product_id}`,
          this.form
        )
        .then(response => {
          console.log(response)
          this.alert = true
          this.isMsg = response.data.msg
          this.getProduct()
        })
        .catch(error => {
          console.log(error.response)
        })
    },
    deleteProduct(product_id) {
      console.log(product_id)
      // axios
      //   .delete(
      //     `${process.env.VUE_APP_URL}/product/${product_id.product_id}`,
      //     this.product_id
      //   )
      //   .then(response => {
      //     console.log(response)
      //   })
      //   .catch(error => {
      //     console.log(error.response)
      //   })
    },
    handlePageChange(numberPage) {
      console.log(numberPage)
      this.page = numberPage
      this.getProduct()
    }
  },
  computed: {
    rows() {
      return this.totalRows
    }
  }
}
</script>

<style></style>
