<template>
  <div>
    <h1 class="h1">
      Where to, silly Traveler?
    </h1>
    <cube :input="input" />
    <formi v-on:submit="onSubmit"/>
    <ul class="list">
      <li v-for="(name, index) in input">
        {{ name }} <span v-on:click="trash(index)"> Löschen </span>
      </li>
    </ul>
  </div>
</template>

<script setup>

const input = ref([])
const onSubmit = (value) => {
  console.log('onSubmit')
  input.value.push(value.value)
}
const trash = (value) => {
  input.value.splice(value,1)
}
</script>

<style lang="scss">
  .h1 {
    text-align: center;
    color: #545F64;
    font-family: Arial, Helvetica, sans-serif;
  }

  .list {
    text-align: left;
    list-style: none;
    font-family: Arial, Helvetica, sans-serif;
    color: #545F64;
    margin-top: 20px;
    line-height: 25px;
    width: 100%;
    max-width: 200px;
    margin: 0 auto;
  }

</style>