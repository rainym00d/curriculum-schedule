<template>
  <div class="schedule">
    <table>
      <thead>
        <tr>
          <th>Monday</th>
          <th>Tuesday</th>
          <th>Wednesday</th>
          <th>Thursday</th>
          <th>Friday</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="i in 7">
          <td v-for="j in 5"  @click="showCourse((i-1)*5+(j-1))">
            <CourseDetail :course="courses[(i-1)*5+(j-1)]" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import CourseDetail from './CourseDetail.vue'

export default {
  props: ['courses'],
  components: {
    CourseDetail
  },
  methods: {
    showCourse(id) {
      this.$emit('show', id)
    }
  }
}
</script>

<style scoped>
  /* .schedule {
    width: 90%;
    padding: 40px;
    margin: 150px auto;
    border-radius: 20px;
    background: white;
  } */
  table {
    table-layout: fixed;
    width: 60%;
    height: 700px;
    margin: 20px auto;
    border-collapse: collapse;
    /* border-width: 1px; */
  }
  th, td {
    border: 1px solid #ccc;
  }
  th {
    height: 50px;
  }
  td {
    height: 90px;
    cursor: pointer;
  }
  td:hover {
    background-color: #ddd;
  }
</style>