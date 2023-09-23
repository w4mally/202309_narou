<script setup lang="ts">
import { computed, ref } from 'vue'

/* 型の定義 */
interface task {
    name: string
    state: boolean 
}

const tasks = ref<task[]>([
    {name: '履修登録', state: false},
    {name: 'バイト先電話', state: true}
])

const finished_task = computed(() => tasks.value.filter((task) => task.state === true))
const not_finished_task = computed(() => tasks.value.filter((task) => task.state === false))

const newtaskName = ref('')

const addtask = () => {
    if( newtaskName.value === '' ) return
    tasks.value.push({ name: newtaskName.value, state: false })
    newtaskName.value = ''
}
</script>

<template>
    <div>
        <h2>ToDoList</h2>
        <div>【未完了のタスク】</div>
        <ul>
         <li v-for="task in not_finished_task" :key="task.name">
            <div>{{ task.name }}</div>
            <div><button @click="task.state = true">完了</button></div>
         </li>
        </ul>
        <div>【完了済みのタスク】</div>
        <ul>
         <li v-for="task in finished_task" :key="task.name">
            <div>{{ task.name }}</div>
         </li>
        </ul>
        <div>
            <label>
                追加したいタスクを入力
                <input v-model="newtaskName" type="text" />
            </label>
            <button @click="addtask">追加</button>
        </div>
    </div>
</template>

<style></style>