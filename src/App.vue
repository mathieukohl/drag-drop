<template>
  <div class="container">
    <div class="list-container">
      <h2>Syllable</h2>
      <ul>
        <draggable class="dragArea list-group w-full" :list="list1" @change="log">
          <li v-for="(item, index) in list1" v-bind:key="index">{{ item }}</li>
        </draggable>
      </ul>
    </div>
    <div class="list-container">
      <h2>JP Characters</h2>
      <ul>
        <draggable class="dragArea list-group w-full" :list="list2" @change="log">
          <li v-for="(item, index) in list2" v-bind:key="index">{{ item }}</li>
        </draggable>
      </ul>
    </div>
  </div>
  <div class="container">
    <div class="list-container">
      <h2>Syllable</h2>
      <ul>
        <draggable class="dragArea list-group w-full" :list="list3" @change="log">
          <li v-for="(item, index) in list3" v-bind:key="index">{{ item }}</li>
        </draggable>
      </ul>
    </div>
    <div class="list-container">
      <h2>JP Characters</h2>
      <ul @drop="drop" @dragover.prevent>
        <draggable class="dragArea list-group w-full" :list="list4" @change="log">
          <li v-for="(item, index) in list4" v-bind:key="index">{{ item }}</li>
        </draggable>
      </ul>
    </div>
  </div>
  <button class="btn_random" @click="randomize">Randomize</button>
</template>

<script>
import { defineComponent } from 'vue';
import { VueDraggableNext } from 'vue-draggable-next';
import data from './assets/data.json'

export default defineComponent({
  components: {
      draggable: VueDraggableNext,
  },
  data() {
    return {
      list1: data.list1,
      list2: data.list2,
      list3: data.list3,
      list4: data.list4,
    }
  },
  mounted() {
    fetch('data.json')
      .then(response => response.json())
      .then(data => {
        this.list1 = data.list1;
        this.list2 = data.list2;
      });
  },
  methods: {
    randomize() {
      this.list1.sort(() => Math.random() - 0.5);
      this.list2.sort(() => Math.random() - 0.5);
      this.list3.sort(() => Math.random() - 0.5);
      this.list4.sort(() => Math.random() - 0.5);
    }
  }
})
</script>

<style>

.list-container {
  float: left;
  width: 50%;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 10px;
  border: 1px solid #ccc;
  margin-bottom: 10px;
  margin-right: 10px;
  background-color: #f9f9f9;
  cursor: move;
}

.btn_random{
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
}
</style>
