<template>
    <div class="inner">
        <Filters />
        <Mapper />
          <InfoPane />
      </div>
    </div>

</template>

<script>
import Mapper from '~/components/Mapper.vue'
import Filters from '~/components/Filters.vue'
import InfoPane from '~/components/InfoPane.vue'

export default {
  components: {
    Mapper,
    Filters,
    InfoPane
  }
}
</script>

<style>



</style>
