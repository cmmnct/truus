<script setup lang="ts">
import { ref, onMounted } from 'vue';
import MemoryCard from '../components/MemoryCard.vue';

export type card = {
  set: string;
  turned: boolean;
  hidden: boolean;
  card1?: string;
  card2?: string;
}

export type customer = {
  name: string;
  function: string;
  invited?: boolean;
  confirmed?: boolean;
  declined?: boolean;
  partner: string;
  allergies: string[];
}

const cards = ref<card[]>([])
let animals: card[] = [];

onMounted(() => {
  console.log("Component mounted");
  fetch("https://my-json-server.typicode.com/cmmnct/cards/cards")
    .then(response => response.json())
    .then(data => {
      animals = data;
      cards.value = [];
      animals.map(item => cards.value.push(
        {
          set: item.set,
          turned: false,
          hidden: false
        }
      ));
    })
    .catch(error => console.error('Error fetching data:', error));

});

const customerdata = [
  {
    name: "Alice Smith",
    function: "Designer",
    declined: true,
    invited: true
  },
  {
    name: "Bob Johnson",
    function: "Project Manager",
    confirmed: true
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
    invited: item.invited || false,
    confirmed: item.confirmed || false,
    declined: item.declined || false,
    partner: "",
    allergies: []
  }
));






const remind = (name: string) => {
  alert(`Reminder sent to ${name}`);
}

function onClickCard(currentCard: card) {
  if (currentCard.turned) {
    return
  } else {
    currentCard.turned = true;
  }
  console.log(currentCard);
}

</script>

<template>
  <main>
    <div class="cardgrid">
      <MemoryCard @click="onClickCard(currentCard)" v-for="currentCard in cards" :key="currentCard.set"
        :MemoryCard="currentCard" />
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
<style scoped>
.cardgrid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
}
</style>
