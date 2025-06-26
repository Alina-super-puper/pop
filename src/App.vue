<script setup>
import { ref, reactive } from "vue";
// Записываем сюда информацию
const iform = reactive({
  name: "",
  gen: "",
  age: ""
})
// Записываем сюда ошибки
const error = reactive({
  ername: "",
  ergen: "",
  erage: ""
})

// для вывода
const user=ref(null)

// ВАЛИДАЦИЯ

// на имя
function validname() {
  const regname = /^[А-ЯЁ][а-яё]+$/;
  return regname.test(iform.name)
}
// на возраст
function validage(){
  const regage = Number(iform.age)
  return Number.isInteger(regage) && regage >=10 && regage<=100;
}
// на пол
function validgen(){
  return ["ж", "м"].includes(iform.gen);
}
function registr(){
  // очищаем ошибки 
  error.ername="";
  error.erage="";
  error.ergen=""

  if (!validname()) error.ername = "Имя должно быть таким то таким то"
  if (!validgen()) error.ergen="блабла"
  if (!validage()) error.erage ="ой ой ой ой ой"

// если хоть одна ошибка есть то ретурн
  if (error.ername || error.ergen || error.erage) return;

// сохраняем результат
user.value={
  Name: iform.name,
  Gender: iform.gen,
  Age: iform.age
}

iform.name =""
iform.gen=""
iform.age=""


}
</script>

<template>
  <div class="form">
    <h2>Регитсрация</h2>
    <!-- имя -->
    <input class="name" v-model="iform.name" type="text "placeholder="Введите имя">
    <p v-if="error.ername">{{ error.ername }} </p>
     <!-- возраст -->
    <input class="age" v-model="iform.age" type="number"  placeholder="Введите возраст">
    <p v-if="error.erage">{{ error.erage }}</p>
    <!-- пол -->
     <div class="gen">
      <label for=""><input type="radio" value="ж"  v-model="iform.gen" >Ж</label>
      <label for=""><input type="radio" value="м" v-model="iform.gen">М</label>
      <p v-if="error.ergen">{{ error.ergen }}</p>
     </div>
  </div>
<div>
  <button @click="registr" >Завершить</button>
</div>


  <!-- вывод информации -->
   <div v-if="user">
    <h2>Добро пожаловац</h2>
    <p>Имя: {{ user.Name }}</p>
    <p>пол: {{ user.Gender }}</p>
    <p>возраст: {{ user.Age }}</p>
   </div>
</template>

<style scoped>
.form{
  background: rgba(102, 51, 153, 0.205);
  width: 500px;
  color: azure;
  height: 500px;
  display: flex;
  flex-direction: column;

}
.name{
  padding: 8px;
  font-size: 16px;
  width: 200px;
  box-sizing: border-box;
  align-items: center;
}
</style>
