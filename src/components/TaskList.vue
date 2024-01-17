<template>
    <div class="wrapper">
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Time</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(task, index) in tasks" :key="index">
                    <td>{{ task.name }}</td>
                    <td>{{ task.time }} minutes</td>
                    <td> <button @click="openEditPopup(index)">Edit</button></td>
                </tr>
            </tbody>
        </table>
        <div v-if="isEditPopupVisible">
            <div class="edit-popup">
                <div class="form-wrapper">
                    <h2>Edit Task</h2>
                    <form @submit.prevent="updateTask" class="">
                        <div style="margin-bottom: 10px;">
                            <label for="editName">Name:</label>
                            <input v-model="editedTask.name" type="text" id="editName" required>
                        </div>

                        <div>
                            <label for="editTime">Time:</label>
                            <input v-model="editedTask.time" type="number" id="editTime" required>
                        </div>

                        <button type="submit">Submit</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';


const tasks = ref([
    { name: 'Task 1', time: 30 },
    { name: 'Task 2', time: 40 },
    { name: 'Task 3', time: 60 },
    { name: 'Task 4', time: 45 },
    { name: 'Task 5', time: 50 },
]);

const isEditPopupVisible = ref(false);
const editedTask = ref({ name: '', time: 0 });
let editedTaskIndex = null;

const openEditPopup = (index) => {
    editedTask.value = { ...tasks.value[index] };
    editedTaskIndex = index;
    isEditPopupVisible.value = true;
};

const updateTask = () => {
    if (editedTaskIndex !== null) {
        tasks.value[editedTaskIndex] = { ...editedTask.value };
        closeEditPopup();
    }
};

const closeEditPopup = () => {
    isEditPopupVisible.value = false;
    editedTaskIndex = null;
};


</script>
  
<style scoped>
.wrapper {
    width: 800px;
}

.edit-popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: #0707075b;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.form-wrapper {
    width: 35%;
    margin: 0 auto;
    padding: 20px;
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 10px;
}

.form-wrapper h2 {
    color: #000;
    margin: 0;
    margin-bottom: 15px;
}

.form-wrapper label {
    color: #000;
    margin-bottom: 8px;
    display: block;

}

.form-wrapper form {
    width: 100%;
}

button {
    border-radius: 8px;
    border: 1px solid transparent;
    padding: 0.5em 1.2em;
    font-size: 14px;
    font-weight: 500;
    font-family: inherit;
    background-color: #255594;
    cursor: pointer;
    transition: border-color 0.25s;
}

button:hover {
    border-color: #646cff;
}

button:focus,
button:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
}

.form-wrapper button {
    margin-top: 15px;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;

}

th,
td {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: center;
}

th {
    background-color: #0c0c0c;

}

tr {
    transition: all .4s ease-in;
}

tr:hover {
    background-color: #0e0d0df5;
}

input {
    width: 96%;
    padding: 15px 10px;
    border-radius: 8px;
    outline: none;
    border: 1px solid #888;
    background: transparent;
    color: #000;
}
</style>
  