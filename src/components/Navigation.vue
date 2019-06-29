<template>
  <div id="nav">
    <ul>
      <li>簡易メモ帳</li>
      <li><button @click="onNew">新規作成</button></li>
      <li>
        <select v-model="selected">
          <option
              v-for="memo in memos"
              :key="memo.id"
              :value="memo.id"
          >
            {{ memo.title }}
          </option>
        </select>
        <button @click="onOpen(selected)">を開く</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Navigation',
  props: {
    memos: Array,
    onNew: Function,
    onOpen: Function
  },
  data() {
    return {
      selected: this.memos[0]
    }
  }
}
</script>

<style scoped>
#nav {
  width: 100%;
}

ul {
  list-style-type: none;
  border-bottom: lightgray 1px solid;
  padding: 1em;
  display: flex;
  justify-content: space-evenly;
  width: 100%;
}
</style>

