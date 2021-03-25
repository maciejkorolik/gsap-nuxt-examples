<template>
  <section class="pt-24">
    <div class="text-center">
      <h2 class="text-6xl mb-10">
        <span
          v-for="(letter, i) in title"
          ref="letter"
          :key="letter + i"
          class="inline-block"
          >{{ letter }}</span
        >
      </h2>
    </div>
    <div class="w-3/5 mx-auto grid grid-auto-flow grid-cols-10 gap-4 mb-16">
      <div
        v-for="(n, i) in 60"
        ref="box"
        :key="n"
        class="h-16 bg-orange-400 cursor-pointer"
        @click="playAnimation(i)"
      />
    </div>
    <div class="flex justify-between h-64 mb-6">
      <div
        v-for="n in 100"
        ref="wave"
        :key="n"
        class="h-64 flex-1 mx-1 rounded-md bg-purple-400"
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
      title: 'Staggers'.split(''),
    }
  },
  mounted() {
    gsap
      .timeline()
      .from(this.$refs.letter, {
        y: -150,
        ease: 'elastic',
        duration: 2,
        stagger: {
          from: 'start',
          grid: 'auto',
          each: 0.05,
        },
      })
      .from(
        this.$refs.letter,
        {
          opacity: 0,
          duration: 0.4,
        },
        0
      )

    gsap.set(this.$refs.wave, {
      transformOrigin: 'center center',
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
