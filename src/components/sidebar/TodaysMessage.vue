<template>
  <div class="todays-message-container">
    <div class="todays-message">
        No lesson for today yet...
    </div>
    <div class="add-lesson-button" v-on:click="addLessonClicked">
        Add Today's Lesson
    </div>
  </div>
</template>

<script>
export default {
    name: 'TodaysMessage',
    components: {
    },
    methods: {
        addLessonClicked: function() {
            this.$emit("addLessonClicked");
        }
    },
}
</script>

<style scoped>
.todays-message-container {
    padding: 1rem;
}

.todays-message {
    color: var(--text-colour-light);
}

.add-lesson-button {
    margin-top: 1rem;
    padding: 1rem;

    text-align: center;
    color: var(--text-colour-dark);
    background-color: var(--colour-secondary);
    border-radius: 0.25rem;
    
    cursor: pointer;
}
</style>
