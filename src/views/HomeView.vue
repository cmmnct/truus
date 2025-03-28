<script setup lang="ts">
import { ref } from 'vue';

type card = {
  set: string;
  turned: boolean;
  hidden: boolean;
  card1?: string;
  card2?: string;
}

type customer = {
  name: string;
  function: string;
  invited?: boolean;
  confirmed?: boolean;
  declined?: boolean;
  partner?: string;
  allergies?: string[];
}

const customerdata = [
  {
    name: "Alice Smith",
    function: "Designer",
  },
  {
    name: "Bob Johnson",
    function: "Project Manager",
  },
  {
    name: "Charlie Brown",
    function: "QA Engineer",
  },
  {
    name: "Diana Prince",
    function: "Frontend Developer",
  },
  {
    name: "Ethan Hunt",
    function: "Backend Developer",
  },
  {
    name: "Fiona Gallagher",
    function: "DevOps Engineer",
  }
];

const customers = ref<customer[]>([])
customerdata.map(item => customers.value.push(
  {
    name: item.name,
    function: item.function,
    invited: false,
    confirmed: false,
    declined: false,
    partner: "",
    allergies: []
  }
));

const animals = ["hen", "dog", "chick", "kitten", "veal", "horse"];

const cards = ref<card[]>([])

animals.map(item => cards.value.push(
  {
  set: item,
  turned: false,
  hidden: false
}
));

</script>

<template>
  <main>
    <div v-for="card in cards" :key="card.set">
      <img :src="'/img/' + card.set + '.webp'" :alt="card.set">

    </div>
    <div>
      <table>
        <tr>
            <th>Name</th>
            <th>Function</th>
            <th>Invited</th>
            <th>Confirmed</th>
            <th>Declined</th>
            <th>Partner</th>
            <th>Allergies</th>
            <th>Invite</th>
            <th>remind</th>
        </tr>
        <tr v-for="customer in customers" :key="customer.name">
        <td>{{ customer.name }}</td>
        <td>{{ customer.function }}</td>
        <td><input type="checkbox" disabled :checked="customer.invited"></td>
        <td><input type="checkbox" disabled :checked="customer.confirmed"></td>
        <td><input type="checkbox" disabled :checked="customer.declined"></td>
        <td><input type="text" disabled :value="customer.partner"></td>
        <td><input type="text" disabled :value="customer.allergies"></td>
        <td><button @click="customer.invited = !customer.invited">Invite</button></td>
        <td><button @click="remind(customer.name)">Remind</button></td>
          </tr>
      </table>
      <button @click="customers.forEach(customer => customer.invited = true)">Invite All</button>
      </div>
  </main>
</template>
