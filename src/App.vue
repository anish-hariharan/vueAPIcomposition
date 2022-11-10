<template>
  <section class="container">
    <UserData :userName="uName" :age="age"></UserData>
    <h2>{{ age.value }}</h2>
    <h1>{{ user.age }}</h1>
    <button @click="setAge">Change Age</button>
    <input type="text" placeholder="First Name" @input="setFirstName">
    <input type="text" placeholder="Second Name" @input="setLastName">
  </section>
</template>

<script>
import { reactive, computed, watch, ref } from "vue";
import UserData from "./components/UserData.vue";
export default {
  components: { UserData }, 
  setup() {
    const user = reactive({
      name: "jackin",
      age: 51, 
      firstName : '',
      secondName: ''
    });
    const age = ref(30)

    setTimeout(function () {
      (user.name = "Anish"), (user.age = 21);
    }, 2000);
    
    // function setNewAge(){
    //   user.age += 10
    // }
    const uName = computed(function () {
      return user.firstName + ' ' + user.secondName
    })

    let setNewAge = () => {
      age.value += 10
    }

    let setFirstName = (event) => {
      user.firstName = event.target.value
    }

    let setLastName = (event) => {
      user.secondName = event.target.value
    }

    watch(age, function(newValue, old) {
      console.log('new value is ' + newValue)
      console.log('old value is ' + old)
    })

    return {
      user: user,
      age: user.age,
      uName : uName,
      setAge: setNewAge,
      setFirstName: setFirstName,
      setLastName: setLastName
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>
