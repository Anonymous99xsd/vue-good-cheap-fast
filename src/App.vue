<template>
    <div id="app">
        <Toggler :size="4" :checked="checked[0]" @updated="value => updateHandler(0, value)">Good</Toggler>
        <Toggler :size="4" :checked="checked[1]" @updated="value => updateHandler(1, value)">Cheap</Toggler>
        <Toggler :size="4" :checked="checked[2]" @updated="value => updateHandler(2, value)">Fast</Toggler>
    </div>
</template>

<script>
import Toggler from './components/Toggler.vue'

export default {
    name: 'App',
    components: {
        Toggler,
    },
    data() {
      return {
        checked: [false, false, false],
        indexes: [],
      }
    },
    methods: {
      updateHandler(index, value) {
        if (value && !this.indexes.includes(index)) {
          let newIndexes = [...this.indexes]
          newIndexes.push(index)
          this.indexes = newIndexes
        }
        if (!value && this.indexes.includes(index)) {
          let newIndexes = [...this.indexes]
          newIndexes.splice(this.indexes.indexOf(index), 1)
          this.indexes = newIndexes
        }
        if (this.indexes.length === 3) {
          let newIndexes = [...this.indexes]
          newIndexes.shift()
          this.indexes = newIndexes
        }
        let checked = [false, false, false]
        if (this.indexes[0] !== undefined) {
          checked[this.indexes[0]] = true
        }
        if (this.indexes[1] !== undefined) {
          checked[this.indexes[1]] = true
        }
        this.checked = checked
      }
    },
}
</script>

<style>
#app {
    font-family: Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    flex-direction: column;
}
</style>
