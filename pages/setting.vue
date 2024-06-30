<template>
    <div>
        <div class="vuejs-container">
            <h1>Setting</h1>
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
