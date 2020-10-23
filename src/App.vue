<template>
  <div id="app">
    <SideBar 
      v-bind:todaysDate="getTodaysDate" 
      v-bind:todayHasLesson="todayHasLesson" 
      v-on:add-lesson-clicked="onAddLessonClicked">
    </SideBar>
    <LessonInputDialog 
      v-if="lessonDialog.isShowing" 
      v-bind:isAddingLesson="lessonDialog.isAddingLesson" 
      v-bind:lessonDate="lessonDialog.lessonDate" 
      v-bind:lessonText="lessonDialog.lessonText" 
      v-on:lesson-input-dialog-dismissed="onLessonInputDialogDismissed"
      v-on:lesson-input-dialog-done="onLessonInputDialogDone">
    </LessonInputDialog>
    <MessageDialog
      v-if="messageDialog.isShowing" 
      v-bind:title="messageDialog.title" 
      v-bind:message="messageDialog.message" 
      v-on:message-dialog-dismissed="onMessageDialogDismissed">
    </MessageDialog>
    <MainContent 
      v-bind:lessons="storedLessons"
      v-on:edit-lesson-clicked="onEditLessonClicked">
    </MainContent>
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

      lessonDialog: {
        isShowing: false,
        isAddingLesson: true,
        lessonDate: "",
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

      this.lessonDialog.isShowing = true;
      this.lessonDialog.isAddingLesson = true;
      this.lessonDialog.lessonDate = getDateString(this.getTodaysDate); // this.getTodaysDate() won't work!
      this.lessonDialog.lessonText = "";
    },
    onEditLessonClicked: function(lesson) {
      console.log(lesson.date);
      console.log(lesson.text);

      this.lessonDialog.isShowing = true;
      this.lessonDialog.isAddingLesson = false;
      this.lessonDialog.lessonDate = lesson.date;
      this.lessonDialog.lessonText = lesson.text;
    },
    onMessageDialogDismissed: function() {
        this.messageDialog.isShowing = false;
        this.messageDialog.title = "";
        this.messageDialog.message = "";
    },
    onLessonInputDialogDismissed: function() {
        this.dismissInputLessonDialog();
    },
    onLessonInputDialogDone: function(addedLesson) {
      // A new lesson is added, so update the UI, save to local storage and remove the add lesson button.
      this.storedLessons.unshift(addedLesson);
      localStorage.setItem(LESSONS_STORAGE_KEY, JSON.stringify(this.storedLessons));
      this.todayHasLesson = true;

      this.dismissInputLessonDialog();
    },
    dismissInputLessonDialog: function() {
      this.lessonDialog.isShowing = false;
      this.lessonDialog.isAddingLesson = true;
      this.lessonDialog.title = "";
      this.lessonDialog.message = "";
    },
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
