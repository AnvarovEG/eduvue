<template>
  <div class="card">
    <div>
      <h3>{{ title }}</h3>
      <app-button @action="open">
        {{ isNewsOpen ? 'Закрыть' : 'Открыть' }}
      </app-button>
      <app-button color="danger" v-if="wasRead" @action="$emit('news-unmark',id)">Отменить прочтение</app-button>
      <div v-if="isNewsOpen">
        <hr/>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio ducimus error quaerat
          recusandae tempora unde.
        </p>
        <app-button color="primary" v-if="!wasRead" @action="mark">Прочесть новость</app-button>
        <app-news-list></app-news-list>
      </div>
    </div>
  </div>
</template>

<script>
import AppButton from "@/AppButton";
import AppNewsList from "@/AppNewsList";

export default {
  name: "AppNews.vue",
  props: {
    id: {
      type: Number,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      validator: (value) => {
        return true || value
      }
    },
    wasRead: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  emits: {
    'news-open': null,
    'news-mark'(id) {
      if (id) {
        return true
      }
      console.warn('Необходимо передать id эмит news-mark')
      return false
    },
    'news-unmark'(id) {
      if (id) {
        return true
      }
      console.warn('Необходимо передать id эмит news-unmark')
      return false
    }
  },
  data() {
    return {
      isNewsOpen: this.isOpen
    }
  },

  methods: {
    open() {
      this.isNewsOpen = !this.isNewsOpen
      if (this.isNewsOpen) {
        this.$emit('news-open')
      }
    },

    mark() {
      this.isNewsOpen = false
      this.$emit('news-mark', this.id)
    }

  },

  components: {AppNewsList, AppButton}
}
</script>

<style scoped>

</style>