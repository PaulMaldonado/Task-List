<template>
  <div>
    <div class="container">
        <div class="row">
            <div class="col-md-5 col-sm-12 col-lg-5 col-xl-5 col-xxl-5 mx-auto">
                <div class="card mt-4 shadow-lg p-3 mb-5 bg-white rounded">
                    <h1 class="h2 text-center title-form">Crear tareas</h1>
                    <div class="card-body">
                        <form @submit.prevent="createTasks">
                            <div class="form-group">
                                <input 
                                type="text" 
                                placeholder="Título"
                                class="form-control"
                                v-model="title"
                                >
                            </div>

                            <div class="form-group mt-4">
                                <input 
                                type="date"
                                placeholder="Fecha"
                                class="form-control"
                                v-model="date"
                                >
                            </div>

                            <div class="form-group mt-4">
                                <textarea 
                                rows="10"
                                placeholder="Descripción"
                                class="form-control"
                                v-model="description"
                                >
                                </textarea>
                            </div>

                            <div class="d-grid gap-2 mt-4">
                                <button class="btn btn-dark">Guardar</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div> 

    <div class="container">
        <div class="row">
            <div 
                class="col-md-4 col-sm-12 col-lg-4 col-xl-4 col-xxl-4" 
                v-for="(task, index) in tasks" 
                :key="task.id">

                <div class="card mt-4 shadow-lg p-3 mb-5 bg-white rounded">
                    <div class="card-body">
                        <h5 class="card-title">{{ task.title }}</h5>
                        <p class="card-text">{{ task.description }}</p>
                        <p><strong>{{ task.date }}</strong></p>

                        <button class="btn btn-danger" @click="deleteTask(index)">
                            Eliminar
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <br><br>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
    name: 'Form',

    setup() {
        const title = ref('');
        const date = ref('');
        const description = ref('');
        const tasks = ref([])


        function createTasks() {
           tasks.value.push({
               title: title.value,
               date: date.value,
               description: description.value
           })

           clearFields();
        }

        function deleteTask(index) {
            tasks.value.splice(index, 1)
        }


        function clearFields() {
            title.value = '',
            date.value = '',
            description.value = ''
        }

        return {
            title,
            date,
            description,
            tasks,
            createTasks,
            deleteTask,
            clearFields
        }
    }
}
</script>

<style scoped>
    .title-form {
        font-size: 2em;
        font-weight: 600;
    }

    .mr {
        margin-left: 10px;
    }
</style>