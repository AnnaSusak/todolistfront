<template>
  <div>
    <div>
      <input type="text" id="titleinput" :value="text">
    </div>
    <button type="button" id="add_edit_btn" class="btn-add" v-on:click="add_or_edit">add</button>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    add_note: Function,
    add: Boolean,
    edit_note: Function
  },
  methods: {
    add_or_edit() {
      console.log(this.add)
      if (this.add) {
        this.add_note()
      } else {
        this.edit_note()
      }
    }
  }
}
</script>

<style scoped>
.btn-add {
  background: #FFCF40;
  background: linear-gradient(0deg, #FFCF40 0%, #FFDC73 100%);
  width: 130px;
  height: 40px;
  line-height: 42px;
  padding: 0;
  color: #FFFF;
  border: none;
  margin: 5px;
}

.btn-add:hover {
  background: #FFFF;
  border: 3px solid #FFCF40;
  color: #FFCF40;
}
</style>

