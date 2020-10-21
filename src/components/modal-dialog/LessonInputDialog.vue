<template>
    <div>
        <div id="lessonInput" class="lesson-input-dialog">
            <div class="dialog-content">
                <div class="content-header">
                    <div class="title">{{getTitle}}</div>
                    <div class="close-button" v-on:click="onEditingLessonCancelled">&times;</div>
                </div>
                <div class="content-body">
                    <div class="content-date">{{lessonDate}}</div>
                    <div class="content-text-area">
                        <form action="/">
                            <div>
                                <textarea id="add-lesson-text-area" ref={textAreaRef} maxLength="500" v-on:change={onLessonTextChanged} placeholder="What did you learn?"></textarea>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "LessonInputDialog",
    props: {
        isAddingLesson: Boolean,
        lessonDate: String,
        lessonText: String
    },
    computed: {
        getTitle: function() {
            return this.isAddingLesson ? "Add Today's Lesson" : "Update Lesson";
        }
    },
    methods: {
        onEditingLessonDone: function() {
            console.log("onEditingLessonDone");
        },
        onDeletingLessonDone: function() {
            console.log("onDeletingLessonDone");
        },
        onEditingLessonCancelled: function() {
            console.log("onEditingLessonCancelled");
        },
        onLessonTextChanged: function() {
            console.log("onLessonTextChanged");
        }
    }
}
</script>

<style scoped>
.lesson-input-dialog {
    display: block;
    position: fixed;
    z-index: 8888;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: var(--background-colour-primary);
    background-color: rgba(0, 0, 0, 0.5);
}

.dialog-content {
    background-color: var(--background-colour-secondary);
    padding: 1rem;
    
    /* Positions dialog in the middle of screen. */
    position: relative;
    top: calc((100% - 40%) / 2);
    left: calc((100% - 40%) / 2);
    width: 40%;
    height: 40%;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: stretch;
}

@media screen and (max-width: 600px) {
    .dialog-content {
        background-color: var(--background-colour-secondary);
        padding: 1rem;
        
        /* Positions dialog in the middle of screen. */
        position: relative;
        top: calc((100% - 80%) / 2);
        left: calc((100% - 80%) / 2);
        width: 80%;
        height: 80%;
    
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: stretch;
    }
}

.content-header {
    text-align: center;

    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;

    padding: 0.5rem;
}

.content-header .title {
    flex: 1;

    color: var(--text-colour-dark);
    font-size: 1.5rem;
    text-align: center;
}

.content-header .close-button {
    font-size: 2rem;
    cursor: pointer;
}

.content-body {
    flex: 1;

    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: stretch;

    padding: 0.5rem;
}

.content-body .content-date {
    text-align: center;
    font-size: 0.75rem;
    padding: 0.5rem;
}

.content-body .content-text-area {
    flex: 1;
}

.content-body .content-text-area * {
    height: 100%;
}

.content-body .content-text-area textarea {
    resize: none;
    width: 100%;
    padding: 1rem;
}

.content-footer {
    text-align: center;

    display: flex;
    flex-direction: row;
    align-items: center;

    padding: 0.5rem;
}

.footer-centred {
    justify-content: center;
}

.footer-spread {
    justify-content: space-between;
}

@media screen and (max-width: 600px) {
    .content-footer {
        text-align: center;
    
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
    
        padding: 0.5rem;
    }

    .content-footer .delete-button {
        margin-top: 0.5rem;
    }
}
.content-footer .ghost-button {
    width: 2rem;
    height: 2rem;
}

.content-footer .submit-button {
    padding: 0.75rem;
    text-align: center;
    color: var(--text-colour-dark);
    background-color: var(--colour-secondary);
    border-radius: 0.25rem;
    cursor: pointer;
    text-transform: uppercase;
}

.content-footer .delete-button {
    display: flex;
    flex-direction: column;
    justify-content: center;

    width: 2rem;
    height: 2rem;

    font-size: 1rem;
    text-align: center;
    color: var(--text-colour-dark);
    
    cursor: pointer;
}
</style>