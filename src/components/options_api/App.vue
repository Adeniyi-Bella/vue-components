<template>
  <div v-if="selectedBook" class="p-10">
    <div>
      <img :src="selectedBook.image" />
    </div>
    <div class="my-3">
      <span class="font-bold">Title: </span>
      <span>{{selectedBook.title}}</span>
    </div>
    <div>
      <span class="font-bold ">Author: </span>
      <span>{{selectedBook.author}}</span>
    </div>
    <div class="my-4">
      <span class="font-bold">Publisher: </span>
      <span>{{selectedBook.publisher}}</span>
    </div>
    <button 
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 my-2 px-4 rounded"
      @click="backClick">Back</button>
  </div>
  <div v-else class="p-5 grid grid-cols-4 gap-4">
    <BookCard v-for="book in books" :key="book.id" :book="book" @bookClick="bookClick"/>
  </div>
</template>

<script>
import BookCard from './BookCard.vue'

export default {
  components: {
    BookCard
  },
  data() {
    return {
      books: [],
      selectedBook: null
    }
  },
  mounted() {
    fetch("https://openlibrary.org/search.json?q=star+wars")
      .then(response => response.json())
      .then(data => {
        const booksFromApi = data.docs.map(doc => {
          return {
            id: doc.key,
            title: doc.title,
            image: `https://covers.openlibrary.org/b/id/${doc.cover_i}-L.jpg`,
            author: doc.author_name?.[0]
          }
        })
          
        this.books = booksFromApi
      })
  },
  methods: {
    bookClick(book) {
      this.selectedBook = book
    },
    backClick() {
      this.selectedBook = null
    }
  }
}
</script>

