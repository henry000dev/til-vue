<template>
  <div class="main-content">
    <Header></Header>
    <div class="lessons-container">
      <LessonsList v-bind:lessons="lessons" v-on:edit-lesson-clicked="onEditLessonClicked"></LessonsList>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from './Header';
import LessonsList from './LessonsList';
import Footer from './Footer';

export default {
    name: 'MainContent',
    components: {
      Header,
      LessonsList,
      Footer
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
.main-content {
    /* Use absolute so the left value can be adjusted to be next to the left panel. */
    position: absolute;

    /* The left value should match with the width of left panel. */
    /* left: 20vw; */
    left: 20rem;

    width: calc(100% - 20rem);
    min-height: 100vh;

    background-color: var(--background-colour-secondary);

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;

    padding: 1rem;
}

@media screen and (max-width: 600px) {
    .main-content {
        position: static;

        width: 100%;

        background-color: var(--background-colour-secondary);
    
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
    
        padding: 1rem;
    }
    
}

.lessons-container {
    flex: 1;

    align-self: stretch;

    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
}
</style>
