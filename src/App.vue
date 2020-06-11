<template>
  <div id="app" class="bg-indigo-900 flex flex-col min-h-screen">
    <Header />
    <div class="flex-grow"><router-view /></div>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header'
import Footer from '@/components/Footer'

export default {
  components: {
    Header,
    Footer
  }
}
</script>
