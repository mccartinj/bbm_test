<template lang=pug>
.inner.flex.overflow-hidden
  div(class="w-1/3").text-left.overflow-auto
    SubmitForm
  div(class="w-2/3")
    Mapper

</template>

<script>
import Mapper from '~/components/Mapper.vue';
import SubmitForm from '~/components/SubmitForm.vue'

export default {
  components: {
    Mapper,
    SubmitForm
  }
}
</script>
      

<style lang="scss"> 







</style>
