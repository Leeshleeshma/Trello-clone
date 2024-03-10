<script setup>
import { useBoardStore } from '../stores/boardStore'

const boardStore = useBoardStore()
const route = useRoute()
const router = useRouter()

const newColumnName = ref('')

const isModalOpen = computed(() => {
  return route.name === 'index-tasks-id'
})

function addColumn() {
  boardStore.addColumn(newColumnName.value)
  newColumnName.value = ''
}

function closeModal() {
  router.push('/')
}
</script>

<template>
  <nav>
    <div class="container">
        <h1>Trello Clone</h1>
    </div>
  </nav>
  <div class="board-wrapper">
    <main class="board">
      <BoardColumn
        v-for="(column, columnIndex) in boardStore.board.columns"
        :key="column.id"
        :column="column"
        :columnIndex="columnIndex"
      />
      <UContainer class="column">
        <UInput
          v-model="newColumnName"
          type="text"
          placeholder="Create new column"
          icon="i-heroicons-plus-circle-solid"
          @keyup.enter="addColumn"
        />
      </UContainer>
    </main>
    <div v-show="isModalOpen" class="task-bg" @click.self="closeModal">
      <NuxtPage :key="route.fullPath" />
    </div>
  </div>
</template>

<style>
    nav{
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 75px;
      padding: 5px 70px;
      box-sizing: border-box;
      background: rgba(0,0,0,0.3);
      border-bottom: 1px solid #fff;
    }
    .container{
      width: 100%;
      text-align: center;
      background-color: h-14 bg-gradient-to-r from-purple-500 to-pink-500;
      opacity: 1;
      margin: 0 auto;
      padding: 30px 10%;
      font-family: Arial, sans-serif;
    }
    h1{
        color: black;
        font-size: large;
        font-style: bold;
        position: relative;
    }
    .board{
        display: flex;
        grid: auto / auto auto auto auto;
        margin-top: 130px;
    }
    .column{
        padding: 10px;
        color: black;
        background-color: #020617;
        opacity: 1.0;
    }
    h2{
        color: whitesmoke;
        text-align: left;
        margin-bottom: 5px;
    }
    .h-14{
        opacity: 0.9;
    }
    .font{
        color: black;
    }
</style>