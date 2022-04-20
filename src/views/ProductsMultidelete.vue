<!-- <template>
  <div>
    <VueMultiselect v-model="selected" :options="options">
      :multiple="true"
    </VueMultiselect>
    selected: {{ selected }}
    <button v-on:click="deleteProducts()">delete all</button>
  </div>
</template>

<script>
import VueMultiselect from 'vue-multiselect'
import axios from 'axios'

export default {
  components: { VueMultiselect },
  methods: {
    deleteProducts: function () {
      console.log("deleting products...");
      console.log(this.selected);
      axios.delete("/products/multidelete.json", { data: { products: } }).then((response) => {
        console.log(response.data);
        this.$router.push("/")
      })
    }
  },
  created: function () {
    axios.get('/products.json?simple=true').then((response) => {
      console.log(response.data);
      this.options = response.data;
    })
  },
  data() {
    return {
      selected: null,
      options: []
    }
  }
}
</script>

<style src="vue-multiselect/dist/vue-multiselect.css">
</style> -->