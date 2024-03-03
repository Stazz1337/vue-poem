<script setup>
import { ref } from 'vue';

const props = defineProps({
  quatrains: Array,
});

// состояния видимости для каждого четверостишья

const quatrainVisibility = ref(Array(props.quatrains.length).fill(true));

// счетчик количества нажатых чекбоксов

const checkedCount = ref(0);

// функция переключения видимости четверостишьей

const toggleVisibility = (index, event) => {
  if (!event.target.checked) {
    checkedCount.value++;
    quatrainVisibility.value[index] = false;
  } else {
    checkedCount.value--;
    quatrainVisibility.value[index] = true;
  }
};
</script>

<template>
  <div class="container">
    <header class="header">
      <h1 class="title">Invictus</h1>
      <p class="author">By William Ernest Henley</p>
    </header>

    <main class="main">
      <div class="buttons">
        <div v-for="(visible, index) in quatrainVisibility" :key="index">
          <label>
            <input
              class="button"
              type="checkbox"
              :checked="visible"
              :disabled="checkedCount >= quatrainVisibility.length - 1 && quatrainVisibility[index]"
              @change="toggleVisibility(index, $event)" />
            <span></span>
          </label>
        </div>
      </div>

      <div сlass="poem">
        <div v-for="(quatrain, index) in props.quatrains" :key="index">
          <pre class="quatrain" v-show="quatrainVisibility[index]">
          {{ quatrain }}
        </pre
          >
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped>
.container {
  margin-top: 5%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2rem;
}

.header {
  display: flex;
  align-items: end;
  justify-content: center;
  margin-left: 40%;
}

@media screen and (max-width: 1100px) {
  .header {
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    margin-left: 0;
  }
}

.title {
  font-size: 4rem;
  line-height: 80%;
}

.author {
  font-size: 1.5rem;
  margin-left: 2rem;
}

.poem {
  display: flex;
  flex-direction: column;
}

.quatrain {
  font-size: 2rem;
  min-width: 55rem;
}

.main {
  display: flex;
}

@media screen and (max-width: 1100px) {
  .main {
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
  }
}

.buttons {
  display: flex;
  gap: 1rem;
}

label {
  position: relative;
  cursor: pointer;
}

span {
  width: 2rem;
  height: 2rem;
  border: 1px solid black;
  display: block;
}

input {
  display: none;
}

input:checked ~ span {
  background-color: black;
}
</style>
