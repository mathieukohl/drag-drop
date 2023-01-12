<template>
  <div class="container">
    <div class="list-container">
      <h2>Syllable</h2>
      <ul>
        <draggable v-model="list1" @start="drag=true" @end="drag=false">
          <li v-for="(item, index) in list1" v-bind:key="index">{{ item.name }}</li>
        </draggable>
      </ul>
    </div>
    <div class="list-container">
      <h2>JP Characters</h2>
      <ul>
        <draggable v-model="list2" @start="drag=true" @end="drag=false">
          <li v-for="(item, index) in list2" v-bind:key="index">{{ item.name }}</li>
        </draggable>
      </ul>
    </div>
</div>
  
  <button class="btn_random" @click="randomize">Randomize</button>

  <div class="box">
      <div class="title">Transition Box</div>
      <draggable
        v-model="storage"
        group="list-group"
        class="draggable"
      >
      <li class="item" v-for="(item, index) in storage" v-bind:key="index">{{ item.name }}</li>
      </draggable>
  </div>
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
      storage: []
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
    }/*,
    dragStart(event, item) {
      event.dataTransfer.setData("text/plain", item);
    },
    dragEnd(event) {
      event.dataTransfer.clearData();
    },
    drop(event) {
      const data = event.dataTransfer.getData("text/plain");
      const from = event.dataTransfer.getData("from");
      this[from] = this[from].filter(i => i !== data);
      this.storage.push(data);
    }
    /*
    drop(event) {
      const data = event.dataTransfer.getData("text/plain");
      const from = event.dataTransfer.getData("from");
      const to = event.currentTarget.parentElement.previousElementSibling.textContent;

      if(from === to) return;

      // if the target is the storage-box
      if(to === 'Storage') {
        this.storage.push(data);
        this[from] = this[from].filter(i => i !== data);
      } else {
        this[from] = this[from].filter(i => i !== data);
        this[to].push(data);
      }
    }*/
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

.transfer-container {
  display: flex;
  flex-direction: column;
}

.box {
  border: 1px solid rgba(168, 168, 168, 0.274);
  margin-bottom: 1em;
  border-radius: 5px;
}

.box .title {
  border-bottom: 1px solid  rgb(238, 238, 238);
  text-align: center;
  padding: 5px 0 5px 0;
  background-color: rgba(250, 250, 251, 1);
}
.box .draggable {
  width: 20em;
  height: 10em;
}

.box .item {
  background-color: lightblue;
  border-bottom: 1px solid rgb(168, 168, 168);
  cursor: default;
  padding-left: 10px;
}
</style>
