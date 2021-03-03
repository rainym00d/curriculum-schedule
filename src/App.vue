<template>
  <h1>Curriculum Schedule</h1>
  <div v-if="showCourse">
    <Course :curID="curID" :courses="courses" @close="toggleCourse" @add="addCourse" @delete="deleteCourse" />
  </div>
  <div v-if="courses">
    <Schedule :courses="courses" @show="toggleCourse" />
  </div>
</template>

<script>
import Course from './components/Course.vue'
import Schedule from './components/Schedule.vue'


export default {
  name: 'App',
  data() {
    return {
      showCourse: false,
      courses: null,
      curID: null
    }
  },
  components: {
    Course,
    Schedule
  },
  methods: {
    toggleCourse(id) {
      this.curID = id
      this.showCourse = !this.showCourse
    },
    addCourse(course) {
      var id = this.curID
      this.courses[id] = course
      this.showCourse = !this.showCourse
    },
    deleteCourse() {
      var id = this.curID
      this.courses[id] = {name: '', teacher: '', location: ''}
      this.showCourse = !this.showCourse
    }
  },
  mounted() {
    fetch('http://localhost:3000/courses/')
      .then(res => res.json())
      .then(data => this.courses = data)
      .catch(err => console.log(err.message))
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
body {
  background: #eee;
}
button {
  background: #03cfb4;
  border: none;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}
</style>
