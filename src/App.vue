<template>
  <VueSelectInput :items="items" @selected="selectedItem === $event" />
</template>

<script>
import VueSelectInput from './components/VueSelectInput.vue'

export default {
  name: 'App',
  components: {
    VueSelectInput
  },
  data() {
    return {
      items: [
        {
          id: 1,
          name: 'John Doe',
          email: '',
        },
        {
          id: 2,
          name: 'Jane Doe',
          email: '',
        },
        {
          id: 3,
          name: 'John Smith',
          email: '',
        },
        {
          id: 4,
          name: 'Jane Smith',
          email: '',
        },
        {
          id: 5,
          name: 'Peter Jenkins',
          email: '',
        },
        {
          id: 6,
          name: 'Peter Parker',
          email: '',
        },
        {
          id: 7,
          name: 'Peter Pan',
          email: '',
        },
        {
          id: 8,
          name: 'Peter Griffin',
          email: '',
        },
        {
          id: 9,
          name: 'Peter Quill',
          email: '',
        },
        {
          id: 10,
          name: 'Peter Venkman',
          email: '',
        },
        {
          id: 11,
          name: 'Peter Parker',
          email: '',
        },
        {
          id: 12,
          name: 'Peter Pan',
          email: '',
        },
        {
          id: 13,
          name: 'Peter Griffin',
          email: '',
        },
        {
          id: 14,
          name: 'Peter Quill',
          email: '',
        },
        {
          id: 15,
          name: 'Peter Venkman',
          email: '',
        }
      ],
      selectedItem: null
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
