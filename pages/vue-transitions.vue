<template>
  <section class="pt-24 h-screen">
    <div class="text-center">
      <h2 class="text-6xl mb-10">Vue transitions</h2>
    </div>
    <TodoList class="w-1/3 mx-auto" />
  </section>
</template>

<script>
import gsap from 'gsap'
export default {
  transition: {
    mode: 'out-in',
    css: false,
    beforeEnter(el, done) {
      gsap.from(el, {
        y: -100,
        opacity: 0,
        filter: 'blur(10px)',
        duration: 0.5,
        onComplete: done,
      })
    },
    leave(el, done) {
      gsap.to(el, {
        y: -100,
        opacity: 0,
        filter: 'blur(10px)',
        duration: 0.5,
        onComplete: done,
      })
    },
  },
}
</script>
