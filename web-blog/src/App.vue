<template>
  <div>
    <add-blog></add-blog>
  </div>
</template>

<script>
import addBlog from './components/AddBlog'

export default {
  name: 'App',
  components: {
    'add-blog': addBlog
  },
  data() {
    return {
    }
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: 'Nunito';
  font-weight: 600;
}
</style>
