<template>
  <div>
    <exhibit prefix="experience" :slug="slug" :posts="posts" />
  </div>
</template>

<script>
import Exhibit from '~/components/Exhibit.vue'
export default {
  layout: 'layout-01',
  name: 'Experience',
  components: {
    Exhibit
  },
  props: ['slug'],
  async asyncData() {
    const resolve = require.context('~/posts/', true, /\.md$/)
    const imports = resolve
      .keys()
      .map((key) => {
        const [, slug] = key.match(/\/(.+)\.md$/)
        return Object.assign(resolve(key), { slug })
      })
      .filter((post) => post.attributes.category == 'experience')
    return {
      posts: imports
    }
  }
}
</script>

<style lang="scss">

</style>
