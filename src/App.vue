<template>
  <div id="app">
    <SideBar v-bind:todaysDate="getTodaysDate" v-bind:todayHasLesson="todayHasLesson" v-on:add-lesson-clicked="onAddLessonClicked"></SideBar>
    <LessonInputDialog v-if="lesson.isAddingLesson" v-bind:isAddingLesson="lesson.isAddingLesson" v-bind:lessonDate="lesson.lessonDate" v-bind:lessonText="lesson.lessonText"></LessonInputDialog>
    <MessageDialog v-if="messageDialog.isShowing" v-bind:title="messageDialog.title" v-bind:message="messageDialog.message" v-on:message-dialog-dismissed="onMessageDialogDismissed"></MessageDialog>
    <MainContent v-bind:lessons="storedLessons"></MainContent>
  </div>
</template>

<script>
import SideBar from './components/sidebar/SideBar';
import MessageDialog from './components/modal-dialog/MessageDialog';
import LessonInputDialog from './components/modal-dialog/LessonInputDialog';
import MainContent from './components/main-content/MainContent';
import {getDateString} from './utils/utils';
import DEFAULT_DATA from './data/default.json';

const MAX_LESSON_COUNT = 100;
const LESSONS_STORAGE_KEY = "til-vue.lessons";

// This method is not associated with any Vue instance props/data/state
// etc so can be declared outside of the Vue instance.
function initDefaultLessons() {
  const now = new Date();
  const defaultLessons = [];

  DEFAULT_DATA.forEach(function(lesson, index) {
    const aPreviousDate = (new Date()).setDate(now.getDate() - (index + 1));
    lesson.date = getDateString(new Date(aPreviousDate));
    defaultLessons.push(lesson);
  });

  return defaultLessons;
}

export default {
  name: 'App',
  components: {
    SideBar,
    MessageDialog,
    LessonInputDialog,
    MainContent
  },

  // data returns simple 'state' variables.
  data: function() {
    return {
      todayHasLesson: false,
      storedLessons: [],

      messageDialog: {
        isShowing: false,
        title: "",
        message: ""
      },

      lesson: {
        isAddingLesson: false,
        lessonDate: "01-Oct-2020",
        lessonText: ""
      }
    };
  },

  methods: {
    onAddLessonClicked: function() {
      console.log("Add lesson button clicked!");
      if (this.storedLessons.length >= MAX_LESSON_COUNT) {
        this.messageDialog.isShowing = true;
        this.messageDialog.title = "Add Lesson";
        this.messageDialog.message = "Sorry, cannot add more than " + MAX_LESSON_COUNT + " lessons...\n\nIt's just a demo app after all 😀";
        return;
      }

      this.lesson.isAddingLesson = true;
    },
    onMessageDialogDismissed: function() {
        this.messageDialog.isShowing = false;
        this.messageDialog.title = "";
        this.messageDialog.message = "";
    }
  },

  // computed returns more complex logic for binding. It is "cached" if 
  // the underlying data/state has not changed.
  computed: {
    getTodaysDate() {
      return new Date();
    }
  },

  mounted() {
    // Retrieve lessons from the local storage.
    this.storedLessons = JSON.parse(localStorage.getItem(LESSONS_STORAGE_KEY));

    // If the first time or cache cleared - reload some default lessons. 
    if (!this.storedLessons)
      this.storedLessons = initDefaultLessons();
  }
}
</script>

<style>
/* https://stackoverflow.com/a/55045591/1055373 */
@import './main.css';

#app {
    /* Defines how children elements are laid out. */
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: stretch;
}

/* With mobile screen, just use simple column layout. */
@media screen and (max-width: 600px) {
    #app {
        /* Defines how children elements are laid out. */
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: stretch;
    }
}

</style>
