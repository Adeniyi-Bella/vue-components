<template>
  <div v-if="!book.image.includes('undefined') && book.image" class="mb-15" @click="onBookClick(book)">
    <img :src="book.image" alt="" />
    <div>{{ book.title }}</div>
  </div>
</template>
<script>


export default {
  props: {
    book: {
      type: Object,
      required: true
    },
    onBookClick: {
      type: Function,
      required: true
    }
  }
};
</script>