<template>
  <section class="h-screen pt-24">
    <div class="w-3/5 mx-auto grid grid-auto-flow grid-cols-10 gap-4 mb-16">
      <div
        v-for="(n, i) in 60"
        ref="box"
        :key="n"
        class="h-16 bg-orange-400 cursor-pointer"
        @click="playAnimation(i)"
      />
    </div>
    <div class="flex justify-between h-32">
      <div
        v-for="n in 100"
        ref="wave"
        :key="n"
        class="h-32 flex-1 mx-1 rounded-md bg-purple-400"
      ></div>
    </div>
  </section>
</template>

<script>
import gsap from 'gsap'
export default {
  data() {
    return {
      isPlaying: false,
    }
  },
  mounted() {
    gsap.set(this.$refs.wave, {
      transformOrigin: 'bottom center',
    })
    gsap.from(this.$refs.wave, {
      scaleY: 0.2,
      duration: 0.5,
      stagger: {
        each: 0.02,
        grid: 'auto',
        from: 'center',
        axis: 'x',
        repeat: -1,
        yoyo: true,
      },
      ease: 'sine',
    })
  },
  methods: {
    setAnimationStarted() {
      this.isPlaying = true
    },
    setAnimationCompleted() {
      this.isPlaying = false
    },
    playAnimation(startPoint) {
      if (!this.isPlaying) {
        gsap.to(this.$refs.box, {
          scale: 1.2,
          backgroundColor: '#C6A3CF',
          stagger: {
            each: 0.1,
            grid: 'auto',
            from: startPoint,
            repeat: 1,
            yoyo: true,
          },
          onStart: this.setAnimationStarted,
          onComplete: this.setAnimationCompleted,
        })
      }
    },
  },
}
</script>

<style></style>
