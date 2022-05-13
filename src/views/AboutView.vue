<template>
  <!-- Uzkrauna -->
  <div class="">
    <div v-if="loading">
      <div class="cards">
        <BooksView
          v-for="book in this.books"
          :key="book.id"
          :title="book.name"
          :description="book.description"
        />
      </div>
    </div>
    <div v-else>
      <h1>Tipo loading.... </h1>
    </div>
  </div>
</template>

<script>
//console.log(this.books);
// Defaults
import axios from 'axios';
import BooksView from '@/components/BooksView.vue';
export default {
  name: 'AboutView',
  components: {
    BooksView,
  },
  data() {
    return {
      loading: false,
      books: []
    }
  },
  created() {
    // GET request using axios with set headers
    // .get('http://localhost/shop-api/books')
    // 
    
    this.loading = false;
    axios 
      .get('http://localhost/shop-api/product-latest/')
      .then(response => {
        this.books = response.data.items
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = true);
  },
  mounted () {
    
  },
  methods: {

  }
}
</script>

<style scoped lang="scss">
.cards {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(230px, 1fr));
    grid-gap: 20px;
}
</style>