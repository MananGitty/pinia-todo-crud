<template>
    <form @submit.prevent="handleSubmit"> 
        <input
        type="text"
        placeholder="Write TODO ... "
        v-model="newTask"
        />
        <button >Add Task </button>
    </form>
    
</template>

<script>
import { ref } from '@vue/reactivity'
import { useTaskStore } from '../stores/TaskStore'

export default{

    setup(){
        const taskStore =useTaskStore()
        const newTask=ref('')

        const handleSubmit = () => {
            if (newTask.value.length > 0) {
                taskStore.addTask ({
                    title : newTask.value,
                    isFav:false,
                    id:Math.floor(Math.random()*10000)
                })
                newTask.value=''
            }
        }
    
    
    return{newTask,handleSubmit}
}
}

</script>
