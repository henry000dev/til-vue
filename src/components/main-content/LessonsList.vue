<template>
  <div>
    <Lesson v-for="lesson in lessons" v-bind:key="lesson.date" v-bind:lesson="lesson" v-on:edit-lesson-clicked="onEditLessonClicked"></Lesson>
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
    },
    methods: {
      onEditLessonClicked: function(lesson) {
        this.$emit("edit-lesson-clicked", lesson);
      },
    }
}
</script>

<style>

</style>