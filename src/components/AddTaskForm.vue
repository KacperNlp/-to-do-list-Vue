<template>
    <div class="form-container">
        <form @submit="handleSubmitForm" class="form">
            <label class="label label-of-text">
                <span>Your ticket text:</span>
                <textarea v-model="taskText" cols="100" rows="10"></textarea>
            </label>
            <label class="label label-of-priority">
                <input type="checkbox" v-model="isImportant"/>
                <span>Is this ticket importnat for you?</span>
            </label>
            <button class="button">Add task!</button>
        </form>
    </div>
</template>
<script>
const MAX_VALUE_OF_INDER = 100000;
const generateRandomId = () => {
    return Math.floor(Math.random() * MAX_VALUE_OF_INDER);
}

export default {
    name: 'AddTaskForm',
    emits: ['add-task'],

    data() {
        return {
            taskText: '',
            isImportant: false
        }
    },

    methods: {
        handleSubmitForm(e) {
            e.preventDefault();
            
            const { taskText, isImportant } = this;
            const idOfGeneratedTask = generateRandomId();
            const newTask = {
                text: taskText,
                isImportant,
                id: idOfGeneratedTask
            };

            if(this.checkIfTaskIsAddedCorrectly(newTask)) {
                alert("Sorry you didn't set value of your task or we cannot generate ID");
                return;
            }

            this.resetForm();
            this.$emit('add-task', newTask);
        },

        resetForm() {
            this.taskText = '';
            this.isImportant = false;
        },

        checkIfTaskIsAddedCorrectly(newTask) {
            const { text, id } = newTask;

            if(!text || !id) return true;
            return false;
        }
    }
}
</script>

<style scoped>
.form-container {
    display: flex;
    justify-content: center;
    width: 90%;
    max-width: 600px;
    margin-bottom: 60px;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 20px rgba(0,0,0, .03);
}   

@media (min-width: 768px) {
    .form-container {
        padding: 50px 30px;
    }
}

.form {
    display: flex;
    flex-direction: column;
    align-items: center;
    grid-gap: 25px;
}

.label-of-text {
    display: flex;
    flex-direction: column;
    grid-gap: 10px;
}

.label-of-text textarea {
    width: 100%;
    padding: 10px;
    resize: none;
    background: rgb(240, 240, 240);
    border: 1px solid rgb(215, 215, 215);
}

.label-of-text textarea:focus {
    outline: none;
    border-color: rgb(184, 181, 181);
}

.label-of-priority span {
    padding-left: 5px;
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
</style>