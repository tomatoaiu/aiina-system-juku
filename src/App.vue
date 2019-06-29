<template>
  <div id="app">
    <navigation
      :memos="memos"
      :onNew="newMemo"
      :onOpen="openMemo">
    </navigation>
    <edit-memo
      :memo="currentMemo"
      :onSave="saveMemo"
      :onDelete="deleteMemo">
    </edit-memo>
  </div>
</template>

<script>
import EditMemo from './components/EditMemo.vue'
import Navigation from './components/Navigation.vue'
const DEFAULT_MEMO = {id: -1, title: 'Untitled', content: ''};
const DEFAULT_MEMO_ID = 0;

export default {
  name: 'app',
  components: {
    EditMemo,
    Navigation
  },
  data() {
    return {
      memos: [
        Object.assign({}, DEFAULT_MEMO)
      ],
      maxMemoId: DEFAULT_MEMO_ID,
      currentMemo: Object.assign({}, DEFAULT_MEMO)
    }
  },
  created() {
    this.initMemo();
    this.initMaxMemoId();
  },
  methods: {
    initMemo() {
      if ('memos' in localStorage) {
        this.memos = JSON.parse(localStorage.getItem('memos')) || [DEFAULT_MEMO];
      } else {
        this.memos = [DEFAULT_MEMO];
      }
    },
    initMaxMemoId() {
      if ('maxMemoId' in localStorage) {
        this.maxMemoId = parseInt(localStorage.getItem('maxMemoId')) || DEFAULT_MEMO_ID;
      } else {
        this.maxMemoId = DEFAULT_MEMO_ID;
      }
    },
    saveMemo() {
      if (this.currentMemo.id == -1) {
        this.maxMemoId++;
        this.currentMemo.id = this.maxMemoId;
        this.memos.push(Object.assign({}, this.currentMemo));
      }
      localStorage.setItem('memos', JSON.stringify(this.memos));
      localStorage.setItem('maxMemoId', this.maxMemoId);
    },
    newMemo() {
      this.currentMemo = Object.assign({}, DEFAULT_MEMO);
    },
    openMemo(id) {
      this.currentMemo = this.memos.find((memo) => id === memo.id);
    },
    deleteMemo() {
      const index = this.memos.findIndex((memo) => memo.id === this.currentMemo.id)
      this.$delete(this.memos, index);
      if (this.memos.length < 1) {
        this.newMemo();
      }
      this.saveMemo();
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
