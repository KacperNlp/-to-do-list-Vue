<template>
    <li class="task">
        <p class="task-text">{{ text }}</p>
        <p v-if="isImportant" class="task-important">!</p>
        <div class="task-buttons">
            <button @click="handleDeleteTask" class="button button-delete">Delete</button>
            <button @click="handleChangePriority" class="button">Change Priority!</button>
        </div>
    </li>
</template>
<script>
export default {
    name: 'OneTask',
    inject: ['deleteTask', 'changePriority'],

    props: {
        text: {
            type: String,
            required: true
        },
        id: {
            type: Number,
            required: true
        },
        isImportant: {
            type: Boolean,
            default: false
        }
    }, 

    methods: {
        handleDeleteTask() {
            this.deleteTask(this.id);
        },

        handleChangePriority() {
            this.changePriority(this.id);
        }
    }
}
</script>

<style scoped>
.task {
    position: relative;
    padding: 5px 5px 30px 5px;
    border-bottom: 1px dashed rgb(163, 161, 161);
}

.task-text {
    font-style: italic;
    margin-bottom: 25px;
}    

.task-important {
    position: absolute;
    top: -35px;
    left: -10px;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 30px;
    height: 30px;
    background: rgb(201, 55, 55);
    color: rgb(255, 255, 255);
    border-radius: 50%;
}

.task-buttons {
    display: flex;
    flex-direction: column;
    grid-gap: 10px;
}

@media (min-width: 768px) {
    .task-buttons {
        flex-direction: row;
    }
}
.button {
    padding: 10px 15px;
    background: rgb(101, 136, 100);
    color: rgb(233, 230, 230);
    border: 1px solid rgb(89, 122, 88);
    cursor: pointer;
    transition: .3s;
}

.button:hover {
    background: rgb(233, 230, 230);
    color: rgb(101, 136, 100);
}

.button-delete {
    background: rgb(201, 55, 55);
    border-color: rgb(201, 55, 55);
}

.button-delete:hover {
    color: rgb(201, 55, 55);
}
</style>