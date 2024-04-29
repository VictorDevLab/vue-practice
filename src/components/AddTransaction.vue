<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        type="text"
        id="amount"
        v-model="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";
//for toast notifications
const toast = useToast();

const text = ref("");
const amount = ref("");
///emits
const emit = defineEmits(["transactionSubmitted"]);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Both fields must be filled");
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };
  //emitting event
  emit("transactionSubmitted", transactionData);
  console.log(amount.value);

  text.value = "";
  amount.value = "";
};
</script>
