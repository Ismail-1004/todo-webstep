<template>
  <div class="home">
    <h1 class="home__title"> TODO APP </h1>
    <myForm @submitHandler="addTask" />
    <myList :tasks="tasksList" @deleteTask="deleteTask" v-if="tasksList.length" />
    <h2 class="home__noTask" v-else>Задач пока нету</h2>
  </div>
</template>

<script>
import myForm from "@/components/myForm.vue"
import myList from "@/components/myList.vue"

export default {
  data() {
    return {
      tasksList: [
        { id: 1, title: "Title 1" },
        { id: 2, title: "Title 2" },
        { id: 3, title: "Title 3" }
      ]
    }
  },
  methods: {
    addTask (title) {
      if (title.trim() === "") return

      const task = {
        id: Date.now(),
        title
      }

      this.tasksList.push(task)
      this.setStorage()
    },

    deleteTask(idx) {
      this.tasksList.splice(idx, 1)
      this.setStorage()
    },

    setStorage () {
      localStorage.setItem("tasksList", JSON.stringify(this.tasksList))
    }
  },
  components: {
    myForm,
    myList
  },
  mounted () {
    this.tasksList = JSON.parse(localStorage.getItem("tasksList")) || this.tasksList
  }
}
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;

  &__title {
    text-align: center;
  }
}
</style>
