<template>
  <ListQuotes :quotes="quotes" :listen-quotes="listenQuotes" />
  <div class="mt-2 text-right">
    <cite class="text-small">
      Atualizará novamente em <b>{{ nextUpdateTime }} segundos</b>
    </cite>
  </div>
</template>

<script>
import { ref } from 'vue'
import ListQuotes from './ListQuotes'

export default {
  components: {
    ListQuotes
  },
  props: {
    lintenQuotes: {
      type: Array,
      required: true
    }
  },
  setup() {
    const interval = ref(null);
    const quotes = ref({});
    const nextUpdateTime = ref(30);

    return { quotes, nextUpdateTime };
  }
}
</script>
