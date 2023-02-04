<template>
<AppLayout title ="Task Management">
 <template #header>
            
            <PrimaryButton class="float-right" @click = "createTask">
                Create Task
            </PrimaryButton>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Task Management
            </h2>
          
        </template>
        <table class="table-auto">
  <thead>
    <tr class = bg-green-500 text: white>
      <th>ID</th>
      <th>DESCRIPTION</th>
      <th>STATUS</th>
      <th>ASSIGNEE</th>
      <th>ACTION</th>
    </tr>
  </thead>
  <tbody>
    <tr class="text-center odd:bg-white even:bg-slate-200 hover:bg-blue-500 hover:text-white" v-for="(task,index) in collection.tasks" :key="Index">
      <td>{{ task.id }}</td>
      <td>{{ task.description }}</td>
      <td>{{ task.status_string }}</td>
      <td>{{ task.assignee }}</td>
      <td>
        <div class="flex gap-2 justify-center">
            <SecondaryButton @click="editTask(task.id)">
                Edit
            </SecondaryButton >
            <DangerButton @click="showDeleteDialog">
                Delete
            </DangerButton>
           

        </div>
      </td>
    </tr>

  </tbody>
</table>

<!-- Delete Confirmation Dialog -->
<DialogModal :show="show_delete_dialog" @close="show_delete_dialog = false">
    <template #title>
        <h1>Delete Task</h1>
    </template>
</DialogModal>
</AppLayout>
</template>

<script>
import AppLayout from "@/Layouts/Applayout.vue";
import PrimaryButton from '@/Components/PrimaryButton.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import DangerButton from '@/Components/DangerButton.vue';
import DialogModal from '@/Components/DialogModal.vue';
import {router} from '@inertiajs/vue3'

export default {
    
    components: {
        AppLayout, PrimaryButton, SecondaryButton, DangerButton, DialogModal
    },
    data: function(){
        return{
            show_delete_dialog:false
        }
        
    },
    props: {
        collection:Object
    },
    methods: {
        createTask(){
            router.visit(route('tasks.create'),{method: 'get'})
        },
        editTask(id){
            this.$inertia.visit(route('tasks.edit', id), {method:'get'})
        },
        showDeleteDialog(){
            this.show_delete_dialog = true;
        }
    }
}
</script>