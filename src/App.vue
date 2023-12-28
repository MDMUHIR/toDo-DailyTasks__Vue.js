<script setup>
import { computed, ref } from "vue";

const tasks = ref(["Task 1", "Task 2", "Task 3"]);

const newTask = ref(null);

const searchTask = ref(null);

const filterTasks = computed(() => {
  if (searchTask.value) {
    return tasks.value.filter(
      (task) =>
        task
          .toLocaleLowerCase()
          .indexOf(searchTask.value.toLocaleLowerCase()) !== -1
    );
  } else {
    return tasks.value;
  }
});

const addNewTask = () => {
  if (newTask.value == null) {
    alert("Oops, The input is Empty");
  } else {
    tasks.value.push(newTask.value);
    newTask.value = null;
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};
</script>

<template>
  <div class="container">
    <div class="header w-100 text-center my-5">
      <h1>Muhir's Daily Tasks</h1>
      <div class="search-inp">
        <input
          v-model="searchTask"
          type="text"
          class="form-control"
          placeholder="Search for exist tasks"
        />
      </div>
    </div>

    <div
      class="section d-flex justify-content-center align-items-center flex-column"
    >
      <div class="task-ul mb-5" style="min-width: 500px">
        <ul class="list-group">
          <li
            v-for="(task, index) in filterTasks"
            :key="index"
            class="list-group-item fs-3 text-center poaition-relative px-5"
          >
            <span
              class="fs-4 position-absolute start-0 top-50 translate-middle-y mx-3"
            >
              {{ index + 1 }}
            </span>
            {{ task }}
            <i
              @click="deleteTask(index)"
              class="bi bi-trash3-fill btn btn-sm fs-3 p-0 position-absolute top-50 end-0 translate-middle-y mx-2"
            ></i>
          </li>
        </ul>
      </div>

      <div class="add-inp w-100">
        <label for="at" class="form-label ms-1 fs-3"> Add new task </label>
        <div class="input-group">
          <input
            v-model="newTask"
            @keyup.enter="addNewTask()"
            type="text"
            id="at"
            class="form-control"
            placeholder="Enter a new task here"
          />
          <i
            @click="addNewTask()"
            class="bi bi-plus-circle-fill btn btn-sm btn-success fs-4"
            type="button"
          >
          </i>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
