<template>
<AppLayout title ="Task Management">
 <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Task Management
            </h2>
            <PrimaryButton @click = "createTask">
                Create Task
            </PrimaryButton>
        </template>
        


</AppLayout>
</template>

<script>
import AppLayout from "@/Layouts/Applayout.vue";
import PrimaryButton from '@/Components/PrimaryButton.vue';
import {router} from '@inertiajs/vue3'

export default {
    
    components: {
        AppLayout, PrimaryButton
    },
    methods: {
        createTask(){
            router.visit(route('tasks.create'),{method: 'get'})
        }
    }
}
</script>