<template>
  <div>
    <Lesson v-for="lesson in lessons" v-bind:key="lesson.date" v-bind:lesson="lesson"></Lesson>
  </div>
</template>

<script>
import Lesson from './Lesson';

export default {
    name: 'LessonsList',
    components: {
      Lesson
    },
    props: {
      lessons: Array
    }
}
</script>

<style>

</style>