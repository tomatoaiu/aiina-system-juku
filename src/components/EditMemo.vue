<template>
  <div id="editMemo">
    <ul>
      <li>
        <label>タイトル</label>
      </li>
      <li>
        <input
          id="editMemoTitle"
          type="text"
          v-model="memo.title">
      </li>
      <li>
        <label>メモ</label>
      </li>
      <li>
        <textarea
          id="editMemoContent"
          v-model="memo.content">
        </textareaid=>
      </li>
      <li>
        <div class="buttons">
          <button class="button" @click="onSave">保存する</button>
          <button class="button" @click="onDelete">削除する</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'EditMemo',
  props: {
    memo: Object,
    onSave: Function,
    onDelete: Function
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1em;
}

ul li {
  display: inline-flex;
  width: 100%;
  margin: 0;
  padding: 0;
}

#editMemoTitle {
  flex: 1;
}

#editMemoContent {
  flex: 1;
  height: 20em;
  resize: none;
}

.buttons {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  flex: 1;
}

.button {
  margin: 1em;
  widows: 8em;
}
</style>

