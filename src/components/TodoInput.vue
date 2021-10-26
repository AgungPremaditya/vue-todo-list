<script setup lang="ts"></script>

<template>
  <form class="form-wrapper">
    <label>New ToDo</label>
    <input type="text" name="todo" class="form-input" />
    <input type="submit" value="Add ToDo" class="button" />
  </form>
</template>

<style scoped>
.form-wrapper {
  width: 60%;
  display: flex;
  flex-direction: column;
}
.form-wrapper label {
  color: white;
  margin-bottom: 0.5em;
}
.form-input {
  padding: 1em;
  background: none;
  border-radius: 0.8em;
  border: rgba(255, 255, 255, 0.247) 3px solid;
  color: white;
  font-size: 1em;
}
.form-input:focus-visible {
  outline: none;
}
.button {
  background: #39cbff;
  padding: 1em;
  border: 0;
  margin-top: 1em;
  border-radius: 0.4em;
  width: 100%;
}
</style>
