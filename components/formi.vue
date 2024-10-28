<template>
  <form class="formi__form" v-on:submit.prevent="submit">
    <label class="formi__label">
      Type here and press Submit to summon the internet goblins.
    </label>
    <div class="formi__wrapper">
      <input class="formi__input" v-model="content" type="text" placeholder="Type here...">
      <div class="formi__count">
        {{ content.length }}/20
      </div>
      <button class="formi__button" type="submit">
        Submit
      </button>
    </div>
  </form>
</template>

<script setup lang="ts">
/* ICH DEFINIERE MEINE VARIAVLENS */
const emit = defineEmits(['submit'])
const content = ref('')


/* SOME FUNKTIONEN */
const submit = () => {

  if (content.value.length <= 20) {
    emit('submit', content)
  } else {
    console.log(false)
  }

  content.value = ''
}
</script>

<style lang="scss" scoped>
.formi {
  &__form {
    color: #545F64;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 200px;
    gap: 20px;
  }


  &__label {
    font-family: Arial, Helvetica, sans-serif;
  }

  &__wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: Arial, Helvetica, sans-serif;
  }

  &__input {
    width: 150px;
    height: 30px;
    border-radius: 50px;
    border: 1px solid #545F64;
    text-align: center;
    margin-right: 5px;
    line-height: 30px;
    padding: 0 40px 0 0;

  }

  &__count {
    position: absolute;
    margin: 2px 50px 0 0;
    opacity: 0.4;
  }

  &__button {
    width: 150px;
    height: 30px;
    border-radius: 50px;
    transition: all .5s ease;
    border: 1px solid rgba(110, 126, 133, 0.8);
    background-color: rgba(110, 126, 133, 0.8);
    color: white;
    font-size: 17px;
    line-height: 30px;

    &:hover {
      background-color: #545F64;
    }
  }
}
</style>