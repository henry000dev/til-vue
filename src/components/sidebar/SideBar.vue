<template>
  <div class="sidebar">
    <DateDisplay v-bind:todaysDate="todaysDate"></DateDisplay>
    <TodaysMessage v-if="!todayHasLesson" v-on:add-lesson-clicked="onAddLessonClicked"></TodaysMessage>
  </div>
</template>

<script>
import DateDisplay from './DateDisplay';
import TodaysMessage from './TodaysMessage';

export default {
    name: 'SideBar',
    components: {
      DateDisplay,
      TodaysMessage
    },
    props: {
      todaysDate: Date,
      todayHasLesson: Boolean
    },
    methods: {
      onAddLessonClicked: function() {
        this.$emit("add-lesson-clicked");
      },
  },
}
</script>

<style>
.sidebar {
    /* This make sure the left panel is fixed in place regardless of scroll. */
    position: fixed;

    /* The width should match with the left value of middle panel. */
    width: 20rem;
    height: 100vh;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;

    padding: 2rem 1rem;

    background-color: var(--background-colour-primary);
}

@media screen and (max-width: 600px) {
    .sidebar {
        position: static;

        height: 35rem;
        width: 100%;
    
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
    
        padding: 2rem 1rem;
    
        background-color: var(--background-colour-primary);
    }
}
</style>
