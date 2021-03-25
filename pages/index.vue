<template>
  <div ref="page">
    <section class="h-screen pt-24">
      <div class="relative">
        <div class="absolute inset-0 flex items-center justify-center">
          <h1 ref="title" class="text-6xl uppercase opacity-0">
            GSAP animations
          </h1>
        </div>
        <div class="w-full z-10 grid grid-auto-flow grid-cols-12 gap-2">
          <div
            v-for="n in 60"
            ref="circle"
            :key="n"
            class="h-24 bg-purple-400 rounded-full"
          />
        </div>
        <div ref="arrow" class="absolute bottom-0 w-full text-4xl text-center">
          &darr;
        </div>
      </div>
    </section>
    <section class="h-screen flex flex-col justify-around items-center">
      <div
        ref="image-section"
        class="w-full flex flex-wrap justify-between items-center"
      >
        <p class="w-1/2 p-6">
          Lorem ipsum dolor sit, amet consectetur adipisicing elit. Tempora
          nulla, dignissimos iure est obcaecati aliquam! Ea tempore beatae
          obcaecati totam assumenda quibusdam temporibus, ullam tenetur corrupti
          officiis libero recusandae, quis facere, labore at! Corporis eligendi
          velit eius earum harum dolorum vero fugit aliquam dicta magni maiores,
          aspernatur est ipsum ab.
        </p>
        <img
          class="w-1/2 object-contain p-6"
          src="~/assets/img/michael.gif"
          alt="Michael Scott"
        />

        <img
          class="w-1/2 object-contain p-6"
          src="~/assets/img/michael2.jpg"
          alt="Michael Scott"
        />
        <p class="w-1/2 p-6">
          Lorem ipsum dolor sit, amet consectetur adipisicing elit. Tempora
          nulla, dignissimos iure est obcaecati aliquam! Ea tempore beatae
          obcaecati totam assumenda quibusdam temporibus, ullam tenetur corrupti
          officiis libero recusandae, quis facere, labore at! Corporis eligendi
          velit eius earum harum dolorum vero fugit aliquam dicta magni maiores,
          aspernatur est ipsum ab.
        </p>
      </div>
    </section>
    <section
      ref="horizontal-section"
      class="relative h-screen flex items-center pt-24"
    >
      <div class="absolute inset-0 flex items-center justify-center">
        <div ref="black-circle" class="rounded-full bg-black h-64 w-64" />
      </div>
      <h2 ref="long-text" class="long-text">This text is veeeeeeery long...</h2>
    </section>
    <section ref="bouncing-section" class="h-screen pt-24 relative">
      <div class="absolute w-full bottom-0 flex justify-between h-16">
        <div
          v-for="n in 16"
          :key="n"
          ref="violet-circle"
          class="rounded-full bg-purple-400 h-16 w-16"
        />
      </div>
    </section>
  </div>
</template>

<script>
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

export default {
  mounted() {
    const introTimeline = gsap.timeline()

    gsap.set(this.$refs.title, {
      opacity: 0,
      filter: 'blur(10px',
    })

    gsap.set(this.$refs.arrow, {
      opacity: 0,
    })

    introTimeline
      .to(this.$refs.circle, {
        scale: 0,
        stagger: {
          each: 0.1,
          grid: 'auto',
          from: 'center',
        },
      })
      .to(
        this.$refs.title,
        {
          opacity: 1,
          filter: 'none',
          duration: 1.1,
        },
        '-=1'
      )
      .set(this.$refs.arrow, {
        opacity: 1,
      })
      .to(this.$refs.arrow, {
        y: 3,
        duration: 0.5,
        repeat: -1,
        yoyo: true,
      })

    gsap.from(this.$refs['image-section'].children, {
      opacity: 0,
      x: -40,
      stagger: 0.3,
      duration: 1.5,
      scrollTrigger: {
        trigger: this.$refs['image-section'],
        start: 'top bottom-=300',
      },
    })

    const horizontalTimeline = gsap.timeline({
      scrollTrigger: {
        trigger: this.$refs['horizontal-section'],
        start: 'top top',
        end: '+=500%',
        scrub: true,
        pin: true,
      },
    })

    horizontalTimeline
      .fromTo(
        this.$refs['black-circle'],
        {
          scale: 0,
        },
        {
          scale: 8,
        }
      )
      .fromTo(
        this.$refs['long-text'],
        {
          x: '100vw',
        },
        {
          x: '-200vw',
        },
        '-=0.4'
      )
      .to(
        this.$refs['black-circle'],
        {
          scale: 0.5,
        },
        '-=0.2'
      )

    const bouncingBallsTimeline = gsap.timeline({
      scrollTrigger: {
        trigger: this.$refs['bouncing-section'],
        start: 'top top+=20',
      },
    })

    bouncingBallsTimeline
      .from(this.$refs['violet-circle'], {
        opacity: 0,
        duration: 0.01,
      })
      .from(this.$refs['violet-circle'], {
        y: '-130vh',
        duration: 2,
        ease: 'bounce',
        stagger: {
          from: 'random',
          each: 0.2,
        },
      })
  },
}
</script>

<style>
.long-text {
  font-size: 200px;
  width: 150vw;
  color: white;
  white-space: nowrap;
}
</style>
