<template>
  <div class="backdrop" @click.self="closeCourse">
    <form class="card" @submit.prevent="handleSubmit">

      <label>* course name:</label>
      <input type="text" v-model="course.name" required>

      <label>teacher</label>
      <input type="text" v-model="course.teacher">

      <label>location</label>
      <input type="text" v-model="course.location">

      <div class="buttons">
        <div class="confirm">
          <button>Confirm</button>
        </div>
        <div class="delete">
          <input type="button" value="Delete" @click="handleDelete">
        </div>
      </div>

    </form>
  </div>
</template>

<script>
export default {
  props: ['curID', 'courses'],
  data() {
    return {
      uri: 'http://localhost:3000/courses/' + this.curID,
      course: {
        name: this.courses[this.curID].name,
        teacher: this.courses[this.curID].teacher,
        location: this.courses[this.curID].location
      }
    }
  },
  methods: {
    closeCourse() {
      this.$emit('close')
    },
    handleSubmit() {
      fetch(this.uri, { 
        method: 'PATCH', 
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(this.course) 
      }).then(() => { 
        this.$emit('add', this.course)
      }).catch(err => console.log(err.message))
    },
    handleDelete() {
      fetch(this.uri, { 
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ name: '', teacher: '', location: '' }) 
      }).then(() => { 
        this.$emit('delete')
      }).catch(err => console.log(err.message))      
    }
  }
}
</script>

<style scoped>
  .card {
    width: 300px;
    padding: 40px;
    margin: 150px auto;
    border-radius: 20px;
    background: white;
    text-align: left;
  }
  .backdrop {
    top: 0;
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.8em;
    font-weight: bold;
    letter-spacing: 1px;
    text-transform: uppercase;
  }
  input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  .confirm {
    text-align: center;
  }
  .confirm button {
    width: 100px;
    border: none;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
    background: #0b6dff;
  }
  .delete {
    text-align: center;
  }
  .delete input {
    display: inline-block;
    width: 100px;
    border: none;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
    background: #ff0b0b;
  }
</style>