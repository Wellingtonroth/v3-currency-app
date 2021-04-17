<template>
  <ListQuotes :quotes="quotes" :listen-quotes="listenQuotes" />
  <div class="mt-2 text-right">
    <cite class="text-small">
      Atualizará novamente em <b>{{ nextUpdateTime }} segundos</b>
    </cite>
  </div>
</template>

<script>
import { ref, reactive, toRefs, onMounted } from 'vue'
import ListQuotes from './ListQuotes'
import api from "@/services/api"

export default {
  components: {
    ListQuotes
  },
  props: {
    listenQuotes: {
      type: Array,
      required: true
    }
  },
  setup(props) {
    // const interval = ref(null);
    const quotes = ref({});
    const nextUpdateTime = ref(30);

    const methods = reactive({
      async refresh() {
        const { data } = await api.listen(props.listenQuotes);
        quotes.value = data;
      }
    })

    onMounted(() => {
      methods.refresh()
    })

    return {
      ...toRefs(methods),
      quotes,
      nextUpdateTime
    };
  }
}
</script>
