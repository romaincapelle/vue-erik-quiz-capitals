<template>
  <div class="container mx-auto text-2xl py-8 max-w-xl text-center">
    <h1 class="text-3xl text-white my-12">
      Welcome to the World's Capital Quiz App
    </h1>
    <button
      @click="startQuiz"
      class=" mx-auto bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
    >
      Start Quizz
    </button>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  methods: {
    startQuiz: function() {
      this.$router.push({ path: '/quiz' })
    }
  }
}
</script>
