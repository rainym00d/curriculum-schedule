<template>
  <div>
    <span>{{ course.name }}</span>
    <span>{{ course.teacher }}</span>
    <span>{{ course.location }}</span>
  </div>
</template>

<script>
export default {
  props: ['course'],
}
</script>

<style scoped>
  span {
    display: block;
  }
</style>>
