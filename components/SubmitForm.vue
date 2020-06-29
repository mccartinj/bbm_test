<template lang="pug">
form.bg-white.shadow-xs.rounded.pt-8.px-8.pb-8.mb-4.text
      h2.text-gray-700.mb-10 Submit a Business to 
        nuxt-link(to="/") Shop Black

      label(for="businessname").block.text-gray-700.text-sm.font-bold.mb-2 Business Name
      input(id="businessname" type="text").shadow.appearance-none.border.rounded.w-full.py-2.px-3.text-gray-700.leading-tight
      br
      br

      label(for="category").block.text-gray-700.text-sm.font-bold.mb-2 Category
      .inline-block.relative.w-full
        select(id="category").block.appearance-none.w-full.bg-white.border.border-gray-400.px-4.py-2.pr-8.rounded.shadow.leading-tight
          option Restaurant
          option Fitness
          option Bookstore
        .pointer-events-none.absolute.inset-y-0.right-0.flex.items-center.px-2.text-gray-700
          <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
      br
      br
      label(for="description").block.text-gray-700.text-sm.font-bold.mb-2 Description
      textarea(id="description").shadow.appearance-none.border.rounded.w-full.py-2.px-3.text-gray-700.leading-tight
      br
      br

      label(for="website").block.text-gray-700.text-sm.font-bold.mb-2 Website
      input(id="website" type="text").shadow.appearance-none.border.rounded.w-full.py-2.px-3.text-gray-700.leading-tight
      br
      br

      label(for="phone").block.text-gray-700.text-sm.font-bold.mb-2 Phone Number
      input(id="phone" type="text").shadow.appearance-none.border.rounded.w-full.py-2.px-3.text-gray-700.leading-tight
      br
      br

      label(for="onlinesales").block.text-gray-700.text-sm.font-bold.mb-2 Online Sales?
        span.ml-2
          input(id="onlinesales" type="checkbox").shadow.border.rounded
      br
      br

      input(hidden type="text" id="lat")
      input(hidden type="text" id="lng")

      input(type="submit").bg-blue-500.text-white.font-bold.py-2.px-4.rounded


</template>

export default {
  components: {
    SubmitForm
  }
}
</script>

<style lang="scss">

form {
  h2 {
    font-size: 1.75em;
    font-weight: 700;
  }
}

</style>
