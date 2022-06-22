
pages/index.vue

<template>
  <div>
    <header>
      <div class="head">
        <Logo />
        <b>Books Note</b>
      </div>
    </header>
    <section id="body">
      <p class="top-label">
        You currently have <strong>{{ books.length }}</strong> Books!
      </p>
      <div class="books">
        <div v-for="book in books" :key="book.id">
          <NuxtLink class="link" :to="book.slug.current">
            <div class="book">
              <img
                :src="$urlFor(book.bookcover)"
                :alt="book.bookname"
                loading="lazy"
                class="book-img"
              />
              <div class="book-info">
                <b class="title"> {{ book.bookname }}</b>
                <p class="author">{{ book.author }}</p>
                <p class="desc">
                  {{ book.description }}
                </p>
              </div>
            </div>
          </NuxtLink>
        </div>
      </div>
    </section>
    <footer>
      <NuxtLink to="/about">
        <div class="abt-icon">
          <About />
        </div>
      </NuxtLink>
    </footer>
  </div>
</template>
<script>
import { groq } from "@nuxtjs/sanity";
export default {
  async asyncData({ $sanity }) {
    const query = groq`*[_type == "books"]`;
    const books = await $sanity.fetch(query);
    return { books };
  }
};
</script>