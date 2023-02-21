<script setup lang="ts">
import ToDoItem from "./components/ToDoItem.vue";
import AdderComonent from "./components/AdderComonent.vue";

import axios from "axios";
import {ref, onMounted} from "vue";

interface Item {
  title: string
  id: number
  checked: boolean
}

const notes = ref<Item[]>([]);
let add: Boolean = true;
let cur_id: bigint;
let cur_checked: boolean;

async function get_notes() {
  await axios.get<Item[]>('http://127.0.0.1:8000/items').then((response) => {
    notes.value = response.data
  })
  console.log(notes.value);
}

onMounted(async () => {
  get_notes();
  console.log(notes.value);
});

function delete_note(id: bigint) {
  axios.post('http://127.0.0.1:8000/items/delete', {
    id: id
  })
      .then(function (response) {
        console.log(response);
        get_notes();
      })
      .catch(function (error) {
        console.log(error);
      });
}

function create_note() {
  console.log(1);
  var input = (<HTMLInputElement>document.getElementById('titleinput'));
  axios.post('http://127.0.0.1:8000/items/create', {
    title: input.value
  })
      .then(function (response) {
        console.log(response);
        get_notes();
        input.value = ""
      })
      .catch(function (error) {
        console.log(error);
      });
}

function edit(id: bigint, title: string, checked: boolean) {
  var input = (<HTMLInputElement>document.getElementById('titleinput'));
  input.value = title;
  var button = (<HTMLInputElement>document.getElementById('add_edit_btn'));
  button.textContent = 'edit';
  add = false;
  cur_id = id;
  cur_checked = checked;
  console.log("id: ", id)
  console.log("checked: ", checked)
}

function update_note() {
  var input = (<HTMLInputElement>document.getElementById('titleinput'));
  axios.post('http://127.0.0.1:8000/items/update', {
    title: input.value,
    id: cur_id,
    checked: cur_checked
  })
      .then(function (response) {
        console.log(response);
        console.log("id: ", cur_id)
        console.log("checked: ", cur_checked)
        var button = (<HTMLInputElement>document.getElementById('add_edit_btn'));
        button.textContent = 'add';
        get_notes()
      })
      .catch(function (error) {
        console.log(error);
      });
}

function update_note_checked(id: bigint, title: string, checked: boolean) {
  var input = (<HTMLInputElement>document.getElementById('titleinput'));
  axios.post('http://127.0.0.1:8000/items/update', {
    title: title,
    id: id,
    checked: checked
  })
      .then(function (response) {
        console.log(response);
        console.log("id: ", cur_id)
        console.log("checked: ", cur_checked)
        get_notes()
      })
      .catch(function (error) {
        console.log(error);
      });
}
</script>

<template>
  <div>
    <ul>
      <li v-for="item in notes.valueOf()">
        <ToDoItem :title="item['title']" :id="item['id']"
                  :checked="item['checked']" :key="item['id']" :update="update_note_checked"
                  :delete_funk="delete_note" :edit_btn_clicked="edit"></ToDoItem>
      </li>
    </ul>
  </div>
  <AdderComonent :add_note="create_note" :edit_note="update_note" v-model:add="add"/>
</template>

<style scoped>
li {
  list-style-type: none;
}

div {
  text-align: left;
}
</style>