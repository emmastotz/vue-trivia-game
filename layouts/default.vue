<template>
  <div
    class="bg-scroll bg-center bg-cover h-screen"
    style="background-image: url('underwater.jpg')"
  >
    <header class="blue shadow text-white font-bold">
      <h3 class="text-xl text-center pt-8 tracking-wider">SpongeBob SquarePants Trivia</h3>
      <h6
        class="text-center text-sm font-normal pt-1 pb-8 tracking-wide"
      >&rarr; Who lives in a pineapple under the sea? &larr;</h6>
    </header>
    <nuxt />
  </div>
</template>

<style lang="postcss">
.blue {
  background-color: #0b527a;
}
</style>
