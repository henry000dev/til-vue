<template>
  <div class="lesson-container" v-on:click="onEditLessonClicked">
      <div class="lesson-date">
          {{lesson.date}}
      </div>
      <div class="lesson-text">
           {{lesson.text}}
      </div>
  </div>
</template>

<script>
export default {
    name: 'Lesson',
    components: {
    },
    props: {
        lesson: Object
    },
    methods: {
        onEditLessonClicked: function() {
            this.$emit("edit-lesson-clicked", this.lesson);
        },
    }
}
</script>

<style>
.lesson-container {
    padding: 2rem 0rem;

    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: flex-start;
}

.lesson-date {
    color: var(--colour-primary);
    cursor: pointer;
}
</style>
