<template>
  <q-card class="my-card" bordered v-ripple:primary>
    <q-skeleton height="50px" v-if="load" />
    <q-card-section horizontal v-else>
    <div class="col flex flex-center text-h5">
     {{ count }} - {{ label }}
    </div>
      <q-card-actions vertical class="justify-around q-px-md">
        <q-btn flat round color="primary" :icon="icon" />
      </q-card-actions>
    </q-card-section>
  </q-card>

</template>

<script>
import useAuthUser from "src/composables/UseAuthUser";
import { defineComponent, ref, onMounted} from 'vue'
import useApi from "src/composables/UseApi";

export default defineComponent({
  name: "CardDashbaord",

  props: {
    table: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    icon: {
      type: String,
      required: false,
      default: 'mdi-database-outline'
    }
  },


  setup (props) {
    const count = ref(0)
    const load = ref(true)

    const { user } = useAuthUser()
    const { fetchCount } = useApi()


    onMounted(async () => {
      const response = await fetchCount(props.table, user.value.id)
      count.value = response.count
      load.value = false
    })

    return {
      count,
      load
    }
  }
})
</script>

<style scoped>

</style>
