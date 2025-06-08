<script setup lang="ts">

interface NameProps {
  name: string;
  index: number;
}

const props = defineProps<NameProps>();

const emit = defineEmits(["remove"]);

const removeName = () => {
  emit("remove", props.index);
};

</script>

<template>
  <div class="card">
    <h4>{{ props.name }}</h4>
    <p @click="removeName">x</p>
  </div>
</template>

<style scoped>
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}

.card p {
  position: absolute;
  top: -15%;
  left: 92.5%;
  cursor: pointer;
  color: rgb(160, 157, 157);
}

@media (max-width: 600px) {
  .card {
    width: 45%;
    margin-right: 5px;
    margin-left: 5px;
    padding-right: 2px;
    padding-left: 2px;
  }

  .card p {
    position: absolute;
    top: -18%;
    left: 88.5%;
  }
}
</style>