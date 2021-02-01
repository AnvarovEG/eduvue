<template>
  <div class="container pt-1">
    <div class="card">
      <h2>Актуальные новости на {{ now }}</h2>
      <span>Открыто: <strong>{{ openRate }}</strong> | Прочитано: <strong>{{ readRate }}</strong></span>
    </div>
    <app-news
        v-for="item in news"
        :key="item.id"
        :id="item.id"
        :title="item.title"
        :is-open="item.isOpen"
        :was-read="item.wasRead"
        @news-open="newsOpen"
        @news-mark="newsMark"
        @news-unmark="newsUnmark"
    ></app-news>
  </div>
</template>

<script>
import AppNews from "@/AppNews";

export default {
  data() {
    return {
      now: new Date().toLocaleDateString(),
      openRate: 0,
      readRate: 0,
      news: [
        {
          id: 1,
          title: '1 Lorem ipsum dolor sit amet.',
          isOpen: false,
          wasRead: false
        },
        {
          id: 2,
          title: '2 Lorem ipsum dolor sit amet, consectetur.',
          isOpen: true,
          wasRead: false
        }
      ]
    }
  },
  provide() {
    return {
      news: this.news,
    }
  }
  ,
  methods: {
    newsOpen() {
      this.openRate++
    },

    newsMark(id) {
      const news = this.news.find(el => el.id === id)
      news.wasRead = true
      this.readRate++
    },

    newsUnmark(id) {
      const news = this.news.find(el => el.id === id)
      news.wasRead = false
      this.readRate--
    }

  },

  components: {
    'app-news': AppNews
  }
}
</script>

<style scoped>
h2 {
  color: darkred;
}

h3 {
  color: darkblue;
}

</style>
