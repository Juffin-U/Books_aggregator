<template>
  <div class="books">
    <h3>Прочитанные книги: {{ userLibrary.readBooks.length }}</h3>
    <div class="booksContainer">
      <BookComponent
        v-for="book in userLibrary.readBooks"
        :key="book.id"
        :book="book"
        class="booksComponentContainer"
      ></BookComponent>
    </div>
    <h3>Все мои книги: {{ userLibrary.books.length }}</h3>
    <div class="booksContainer">
      <BookComponent
        v-for="book in userLibrary.books"
        :key="book.id"
        :book="book"
        class="booksComponentContainer"
      ></BookComponent>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { useBooksStore } from "@/store/BooksStore";
import { useUserBooksStore } from "@/store/UserLibraryStore";
import BookComponent from "@/components/BookComponent.vue";

const booksStore = useBooksStore();
const userLibrary = useUserBooksStore();
console.log(userLibrary.books.length);
if (userLibrary.books.length === 0) {
  booksStore.getBooksFromServer();
}
console.log(localStorage.getItem("userBooks"));
</script>
<style scoped>
@media (min-width: 800px) {
}
.books {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.booksContainer {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  max-width: 80%;
  overflow: auto;
  width: 80%;
}

@media (max-width: 800px) {
  .books {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .booksContainer {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    max-width: 80%;
    overflow: auto;
    width: 80%;
  }
}
</style>
