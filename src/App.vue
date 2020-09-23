<template>
  <div class="bg-gray-100 w-screen h-screen">
    <div class="rounded-md shadow-md bg-white px-8 pt-6 pb-8 mb-4 m-auto w-full max-w-xl">
      <form class="px-5" v-on:submit.prevent="addItem">
        <div>
          <label class="block font-bold mb-1" for="input">Item</label>
          <input
            class="shadow appearance-none border border-black rounded-md w-full px-3 text-gray-700 focus:outline-none focus:shadow-outline"
            id="input"
            type="text"
            placeholder="Item"
            v-model="item"
          />
        </div>
        <div>
          <button class="mt-3 shadow appearance-none border border-black rounded-md px-3 w-full font-bold hover:bg-black hover:text-white">
            Add Item
          </button>
        </div>
        <div>
          <button
            @click="deleteAll"
            class="mt-2 shadow appearance-none border border-red-500 bg-red-500 rounded-md px-3 w-full text-white font-bold hover:bg-red-600"
          >
            Delete Items
          </button>
        </div>
      </form>
      <br />
      <div class="px-5">
        <ul class="list-disc">
          <li v-for="(i, index) in items" :key="i.id">
            <div class="mb-1 flex items-center justify-between">
              <h3 @click="toggleToDo(index)" class="cursor-pointer" :class="{ 'line-through': i.done }">{{ i.item }}</h3>
              <button @click="deleteTodo(index)" class="shadow appearance-none broder border-black">
                <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                  <path
                    fill-rule="evenodd"
                    d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
              </button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref } from 'vue';

export default {
  setup() {
    const item = ref(null);
    const items = ref([]);

    const addItem = () => {
      items.value.push({ item: item.value, done: false, id: Date.now() });
      item.value = '';
    };

    const toggleToDo = (index) => {
      items.value[index].done = !items.value[index].done;
    };

    const deleteTodo = (index) => {
      items.value.splice(index, 1);
      document.getElementById('input').focus();
    };

    const deleteAll = () => {
      items.value = [];
      document.getElementById('input').focus();
    };

    return {
      item,
      items,
      addItem,
      toggleToDo,
      deleteTodo,
      deleteAll,
    };
  },
};
</script>
