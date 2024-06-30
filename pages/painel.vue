<template>
  <div>
    <div class="vuejs-container">
      <h1>Painel</h1>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Atque corporis rem ullam deleniti explicabo expedita distinctio, molestiae, voluptatem et recusandae commodi blanditiis veritatis totam architecto debitis. Iste vel itaque necessitatibus!</p>
    </div>
  </div>
</template>

<script>
definePageMeta({
  middleware: [
    function (to, from) {
      // Custom inline middleware
    },
    'auth',
  ],
});
</script>
