<template>
  <div class="container mt-3">
    <div class="card">
      <div class="text-center mt-2">
        <h2>Todo List</h2>
      </div>
      <div class="card-body">
        <div class="mt-2">
          <div class="form-group row">
            <div class="col-9">
              <input type="text" v-model="todoStore.newTask" placeholder="Tambah tugas baru" class="form-control">
            </div>
            <div class="col-3">
              <button class="btn btn-primary w-100" @click="todoStore.addTask">
                <i class="fas fa-plus"></i> Tambah
              </button>
            </div>
          </div>
        </div>
        <div class="mt-3">
          <input type="checkbox" id="hideCompleted" v-model="hideCompleted">
          <label for="hideCompleted">Sembunyikan tugas yang sudah selesai</label>
        </div>
        <div class="table-responsive mt-3">
          <table class="table table-bordered">
            <thead>
              <tr>
                <th style="width: 5%;">No</th>
                <th style="width: 50%;">Tugas</th>
                <th style="width: 20%;">Status</th>
                <th style="width: 25%;">Tindakan</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(task, index) in filteredTasks" :key="index">
                <td>{{ index + 1 }}</td>
                <td :class="{ 'text-decoration-line-through': task.completed }">{{ task.text }}</td>
                <td>
                  <button type="button" class="btn btn-success w-100" @click="todoStore.toggleTaskCompletion(index)">
                    {{ task.completed ? 'Selesai' : 'Belum Selesai' }}
                  </button>
                </td>
                <td>
                  <button type="button" class="btn btn-danger w-100" @click="todoStore.removeTask(index)">
                    <i class="fas fa-trash"></i> Hapus
                  </button>
                </td>
              </tr>
              <tr v-if="filteredTasks.length === 0">
                <td colspan="4">No tasks</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="mt-3">
          <h4>Jumlah tugas yang belum selesai: {{ todoStore.incompleteTasksCount }}</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, ref } from 'vue';
import { useTodoStore } from './store/todo';

export default {
  name: 'App',
  setup() {
    const todoStore = useTodoStore();
    const hideCompleted = ref(false);

    const filteredTasks = computed(() => {
      return hideCompleted.value
        ? todoStore.tasks.filter(task => !task.completed)
        : todoStore.tasks;
    });

    return {
      todoStore,
      hideCompleted,
      filteredTasks
    };
  }
};
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css');
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

/* Gunakan font Poppins untuk seluruh elemen */
body {
  font-family: 'Poppins', sans-serif;
}

/* Contoh penggunaan font Poppins dengan berbagai bobot */
h1, h2, h3, h4, h5, h6 {
  font-family: 'Poppins', sans-serif;
  font-weight: 600; /* Bisa disesuaikan dengan 300, 400, 500, 600, 700 */
}

p, a, span, div {
  font-family: 'Poppins', sans-serif;
  font-weight: 400; /* Bisa disesuaikan dengan 300, 400, 500, 600, 700 */
}

.btn {
  font-family: 'Poppins', sans-serif;
  font-weight: 500; /* Bisa disesuaikan dengan 300, 400, 500, 600, 700 */
}

.text-decoration-line-through {
  text-decoration: line-through;
}

/* CSS untuk input dan tombol */
input[type="text"] {
  border: 1px solid #ced4da;
  border-radius: 4px;
  padding: 8px;
  width: 100%;
  box-sizing: border-box; /* Ensure padding and border are included in the element's width and height */
  transition: border-color 0.3s;
}

input[type="text"]:focus {
  border-color: #007bff;
}

.btn {
  cursor: pointer;
  border-radius: 4px;
  padding: 8px 12px;
  font-size: 14px;
  box-sizing: border-box; /* Ensure padding and border are included in the element's width and height */
  transition: background-color 0.3s, border-color 0.3s;
}

.btn-primary {
  background-color: #007bff;
  border-color: #007bff;
  color: #fff;
}

.btn-primary:hover {
  background-color: #0056b3;
  border-color: #0056b3;
}

.btn-success {
  background-color: #28a745;
  border-color: #28a745;
  color: #fff;
}

.btn-success:hover {
  background-color: #218838;
  border-color: #1e7e34;
}

.btn-danger {
  background-color: #dc3545;
  border-color: #dc3545;
  color: #fff;
}

.btn-danger:hover {
  background-color: #c82333;
  border-color: #bd2130;
}

.w-100 {
  width: 100%;
}

/* CSS untuk tabel */
.table {
  border-radius: 4px;
  width: 100%;
  table-layout: fixed; /* Ensure table does not overflow */
  margin-bottom: 20px; /* Menambahkan ruang bawah 20px */
}

.table thead {
  background-color: #f8f9fa;
}

.table th, .table td {
  border: 1px solid #ced4da;
  padding: 8px;
  overflow-wrap: break-word; /* Ensure long text breaks and does not overflow */
  word-wrap: break-word; 
}

.table th {
  font-weight: bold;
}

.table-bordered {
  border-collapse: collapse;
}

.table-responsive {
  max-width: 100%;
  overflow-x: auto; /* Add horizontal scroll if needed */
}

/* CSS untuk judul */
h2 {
  color: #333;
  margin-bottom: 20px; /* Menambahkan ruang bawah 20px */
}

</style>