<template>
  <div id="app" class="container">
    <div>
      <h2>{{leftLabel}}</h2>
      <input type="text" v-model="searchLeft" placeholder="Search..">
      <select multiple v-model="leftSelectedData" @dblclick="moveRight">
        <option v-for="item in leftData">{{ item }}</option>
      </select>
    </div>

    <div class="middle">
      <button @click="moveRight">=&gt;</button>
      <button @click="moveLeft">&lt;=</button>
    </div>

    <div>
      <h2>{{rightLabel}}</h2>
      <input type="text" v-model="searchRight" placeholder="Search..">
      <select multiple v-model="rightSelectedData" @dblclick="moveLeft">
        <option v-for="item in rightData">{{ item }}</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchLeft: '',
      searchRight: '',
      leftSelectedData: [],
      rightSelectedData: []
    };
  },
  props: {
    leftLabel: {
      type: String,
      required: true
    },
    rightLabel: {
      type: String,
      required: true
    },
    leftData: {
      type: Array,
      required: true
    },
    rightData: {
      type: Array,
      required: true
    },
    searchLeft: {
      type: String,
      required: false
    },
    searchRight: {
      type: String,
      required: false
    },
  },
  methods: {
    moveLeft() {
      if (!this.rightSelectedData.length) return;
      for (let i = this.rightSelectedData.length; i > 0; i--) {
        let idx = this.rightData.indexOf(this.rightSelectedData[i - 1]);
        this.rightData.splice(idx, 1);
        this.leftData.push(this.rightSelectedData[i - 1]);
        this.rightSelectedData.pop();
      }
    },
    moveRight() {
      if (!this.leftSelectedData.length) return;
      for (let i = this.leftSelectedData.length; i > 0; i--) {
        let idx = this.leftData.indexOf(this.leftSelectedData[i - 1]);
        this.leftData.splice(idx, 1);
        this.rightData.push(this.leftSelectedData[i - 1]);
        this.leftSelectedData.pop();
      }
    }
  },
  computed: {
  	filteredLeft() {
      return this.leftSelectedData.filter(leftdata => {
        return leftdata.text.toLowerCase().includes(this.searchLeft.toLowerCase())
      })
    }
  }
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  display: grid;
  grid-template-columns: 30% 10% 30%;
  align-items: center;
}

.container select {
  height: 200px;
  width: 100%;
}

.container .middle {
  text-align: center;
}

.container button {
  width: 80%;
  margin-bottom: 5px;
}
</style>