<template>
    <div>
        <div id="messageDialog" class="messageDialog-dialog">
            <div class="message-dialog-content">
                <div class="message-dialog-content-header">
                    <div class="title">{{title}}</div>
                </div>
                <div class="message-dialog-content-body">
                    <div class="message">{{message}}</div>
                </div>
                <div class="message-dialog-content-footer">
                    <div class="ok-button" v-on:click="onDialogDismissed">OK</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MessageDialog',
    props: {
        title: String,
        message: String
    },
    methods: {
      onDialogDismissed: function() {
        this.$emit("message-dialog-dismissed");
      }
  },
}
</script>

<style scoped>
.messageDialog-dialog {
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

.message-dialog-content {
    background-color: var(--background-colour-secondary);
    padding: 1rem;
    
    /* Positions dialog in the middle of screen. */
    position: relative;
    top: calc((100% - 25%) / 2);
    left: calc((100% - 25%) / 2);
    width: 25%;
    height: 25%;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: stretch;
}

@media screen and (max-width: 600px) {
    .message-dialog-content {
        background-color: var(--background-colour-secondary);
        padding: 1rem;
        
        /* Positions dialog in the middle of screen. */
        position: relative;
        top: calc((100% - 40%) / 2);
        left: calc((100% - 60%) / 2);
        width: 60%;
        height: 40%;
    
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: stretch;
    }
}

.message-dialog-content-header {
    text-align: center;

    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;

    padding: 0.5rem;
}

.message-dialog-content-header .title {
    flex: 1;

    color: var(--text-colour-dark);
    font-size: 1.5rem;
    text-align: center;
}

.message-dialog-content-body {
    flex: 1;

    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: stretch;

    padding: 0.5rem;

    overflow-y: auto;
}

.message-dialog-content-body .message {
    flex: 1;
    height: 100%;

    /* This allows line breaks in string i.e. the \n character. */
    white-space:pre-wrap;
}

.message-dialog-content-footer {
    text-align: center;

    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;

    padding: 0.5rem;
}

.message-dialog-content-footer .ok-button {
    width: 6rem;
    padding: 0.75rem;
    text-align: center;
    color: var(--text-colour-dark);
    background-color: var(--colour-secondary);
    border-radius: 0.25rem;
    cursor: pointer;
}
</style>