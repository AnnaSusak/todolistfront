<script setup lang="ts">
defineProps<{ title: string, id: bigint, checked: boolean, delete_funk: Function, edit_btn_clicked: Function, update: Function }>();
</script>

<template>
  <div>
    <input type="checkbox"
           @change="update(id,title,!checked)" :checked="checked">
    <span>{{ title }}</span>
    <button type="button" class="btn-edit" @click="edit_btn_clicked(id,title,checked)">edit</button>
    <button type="button" class="btn-delete" @click="delete_funk(id)">delete</button>
  </div>
</template>

<style scoped>
.btn-edit {
  background: rgb(0, 172, 238);
  background: linear-gradient(0deg, rgba(0, 172, 238, 1) 0%, rgba(2, 126, 251, 1) 100%);
  width: 60px;
  height: 40px;
  line-height: 42px;
  padding: 0;
  color: #FFFF;
  border: none;
  margin: 5px;

}

.btn-edit:hover {
  background: #FFFF;
  border: 3px solid #007DFF;
  color: #007DFF;
}

.btn-delete {
  background: #FF4040;
  background: linear-gradient(0deg, #FF4040 0%, #FF7373 100%);
  width: 60px;
  height: 40px;
  line-height: 42px;
  padding: 0;
  color: #FFFF;
  border: none;

}

.btn-delete:hover {
  background: #FFFF;
  border: 3px solid #FF4040;
  color: #FF4040;
}
</style>
