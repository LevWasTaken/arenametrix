<template>
<div>
    {{data}}
  <form class="login">
    <div class="identity">
      <input v-model="data.lastName" type="text" placeholder="Nom" />
      <input v-model="data.firstName" type="text" placeholder="Prénom" />
      <input v-model="data.email" type="email" placeholder="Email" />
      <input v-model="data.date" type="date" />
    </div>
    <div class="address">
      <input v-model="data.street" type="text" placeholder="Rue" />
      <input v-model="data.address1" type="text" placeholder="Adresse 1" />
      <input v-model="data.address2" type="text" placeholder="Adresse 2" />
      <input v-model="data.city" type="text" placeholder="Ville" />
      <input v-model="data.postal_code" type="text" placeholder="Code postal" />
      <input v-model="data.country" type="text" placeholder="Pays" />
      <select v-model="data.address_cat" name="address_cat">
           <option v-if="!data.address_cat" disabled :value="null">Type d'adresse</option>
        <option
          v-for="address in address_cat"
          :value="address.id"
          :key="address.id"
        >
          {{ address.label }}
        </option>
      </select>
    </div>
    <div class="tel">
      <input v-model="data.tel" type="text" placeholder="Téléphone" />
      <select v-model="data.tel_cat" name="tel_cat">
          <option v-if="!data.tel_cat" disabled :value="null">Catégorie de tel</option>
        <option
          v-for="(tel, propertyName) in tel_cat"
          :value="tel"
          :key="propertyName"
        >
          {{ propertyName }}
        </option>
      </select>
    </div>
  </form>
  <button v-on:click="onSubmit">Envoyer</button>
  </div>
</template>
<script>
import { ref, onMounted } from "vue";
import axios from "axios";
export default {
  setup() {
    const tel_cat = ref();
    const address_cat = ref();
    const data = ref({
        firstName: null,
        lastName: null,
        email: null,
        date: null,
        street: null,
        address1 : null,
        address2 : null,
        city: null,
        postal_code: null,
        country: null,
        address_cat: null,
        tel: null,
        tel_cat: null,
    })
    
    onMounted(async () => {

      const response = await axios.get("http://localhost:8080/test_vuejs.json");
      tel_cat.value = response.data.tel_cat;
      address_cat.value = response.data.address_cat;
      
    });


    const onSubmit = async () => { 
       const request = await axios.post("https://urldetest.test",{data : data.value})
       console.log(request);
    }

    return {tel_cat, address_cat,data, onSubmit}
  },
};
</script>
<style>
h1 {
  color: red;
}
.login {
  background-color: gray;
  display: flex;
  flex-direction: column;
}
.identity {
  margin-top: 10px;
}
.address {
  margin-top: 10px;
}
.tel {
  margin-top: 10px;
}
</style>