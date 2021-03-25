<template>
  <div class="flex flex-col mb-6">
    <div class="border border-black border-solid mb-4">
      <input
        ref="input"
        v-model="name"
        class="h-12 p-4 w-full focus:outline-none"
        type="text"
        placeholder="Write something and press enter"
        @keydown.enter="handleAddTodo"
      />
    </div>
    <ul>
      <transition-group mode="out-in" @enter="onEnter" @leave="onLeave">
        <li
          v-for="todo in todos"
          :key="todo"
          ref="todo"
          class="w-full bg-orange-200 rounded-xl"
        >
          <div class="p-4 mb-2 flex items-center justify-between">
            <span>{{ todo }}</span>
            <button
              class="h-6 w-6 border border-black border-solid rounded-full focus:outline-none"
              @click="handleRemoveTodo(todo)"
            >
              X
            </button>
          </div>
        </li>
      </transition-group>
    </ul>
  </div>
</template>

<script>
import gsap from 'gsap'
export default {
  data() {
    return {
      name: '',
      todos: [],
    }
  },
  methods: {
    handleAddTodo() {
      const updateList = () => {
        this.todos.push(this.name)
        this.name = ''
      }

      gsap
        .timeline()
        .to(this.$refs.input, {
          opacity: 0,
          filter: 'blur(10px)',
          duration: 0.5,
          onComplete: updateList,
        })
        .to(this.$refs.input, {
          opacity: 1,
          filter: 'none',
        })
    },
    handleRemoveTodo(todoToRemove) {
      this.todos = this.todos.filter((todo) => todo !== todoToRemove)
    },
    onEnter(el) {
      gsap.from(el, {
        opacity: 0,
        duration: 0.3,
      })
      gsap.from(el, {
        x: -50,
        ease: 'elastic',
        duration: 1,
      })
    },
    onLeave(el, done) {
      gsap
        .timeline({
          onComplete: done,
        })
        .to(el, {
          scale: 0.9,
          ease: 'power1',
          duration: 0.2,
        })
        .to(el, {
          opacity: 0,
          scale: 1.5,
          filter: 'blur(10px)',
          duration: 0.4,
        })
    },
  },
}
</script>
