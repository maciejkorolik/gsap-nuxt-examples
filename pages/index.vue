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
        <div
          ref="arrow"
          class="absolute bottom-0 w-full text-4xl text-center opacity-0"
        >
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
          src="https://source.unsplash.com/random/640x320"
          alt=""
        />

        <img
          class="w-1/2 object-contain p-6"
          src="https://source.unsplash.com/random/640x320"
          alt=""
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
      <svg viewbox="-20 0 557 400" width="100%">
        <path
          ref="path"
          fill="none"
          d="M5.176,28.888 C74.169,9.928 66.861,67.129 139.898,66.129 181.135,66.129 193.015,28.297 154.728,26.906 95.82,24.765 96.095,60.961 102.776,76.842 121.363,121.062 217.269,102.111 277.368,98.083 387.377,90.709 356.748,251.201 499.06,230.451 "
        />
        <g ref="plane">
          <path
            fill="#000000"
            d="M31.543,0.16C31.377,0.053,31.188,0,31,0c-0.193,0-0.387,0.055-0.555,0.168l-30,20  c-0.309,0.205-0.479,0.566-0.439,0.936c0.038,0.369,0.278,0.688,0.623,0.824l7.824,3.131l3.679,6.438  c0.176,0.309,0.503,0.5,0.857,0.504c0.004,0,0.007,0,0.011,0c0.351,0,0.677-0.186,0.857-0.486l2.077-3.463l9.695,3.877  C25.748,31.977,25.873,32,26,32c0.17,0,0.338-0.043,0.49-0.129c0.264-0.148,0.445-0.408,0.496-0.707l5-30  C32.051,0.771,31.877,0.377,31.543,0.16z M3.136,20.777L26.311,5.326L9.461,23.363c-0.089-0.053-0.168-0.123-0.266-0.162  L3.136,20.777z M10.189,24.066c-0.002-0.004-0.005-0.006-0.007-0.01L29.125,3.781L12.976,28.943L10.189,24.066z M25.217,29.609  l-8.541-3.416c-0.203-0.08-0.414-0.107-0.623-0.119L29.205,5.686L25.217,29.609z"
          />
        </g>
      </svg>
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
import { MotionPathPlugin } from 'gsap/MotionPathPlugin'

gsap.registerPlugin(ScrollTrigger, MotionPathPlugin)

export default {
  mounted() {
    const introTimeline = gsap.timeline()

    gsap.set(this.$refs.title, {
      opacity: 0,
      filter: 'blur(10px',
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
        start: 'top bottom-=200',
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
          duration: 1,
        }
      )
      .fromTo(
        this.$refs['long-text'],
        {
          x: '100vw',
        },
        {
          x: '-200vw',
          duration: 2,
        },
        '-=0.4'
      )
      .to(
        this.$refs['black-circle'],
        {
          scale: 0.5,
          duration: 1,
        },
        '-=0.4'
      )

    gsap.to(this.$refs.plane, {
      motionPath: {
        path: this.$refs.path,
        align: this.$refs.path,
        alignOrigin: [0.5, 0.5],
        autoRotate: 60,
      },
      scrollTrigger: {
        trigger: this.$refs['bouncing-section'],
        start: 'top center',
        end: 'top top+=20',
        scrub: 0.5,
      },
    })

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
