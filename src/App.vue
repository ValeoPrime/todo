<template>
  <div class="p-grid p-fluid">
    <div class="p-col-12 p-md-12">
      <div class="p-inputgroup">
        <InputText placeholder="Add toDo" v-model="inputValue" />
        <Button label="Add" @click="addToDo" />
      </div>
    </div>
  </div>
  <div
    class="p-flex-column p-mt-4 p-ai-center"
    align="center"
    v-if="toDos.length"
  >
    <Card
      class="p-d-flex p-mb-2"
      v-for="toDo of toDos"
      :key="toDo.id + 1.14"
      :id="toDo.id"
      style="width: 80%"
    >
      <template #title>
        {{ toDo.title }}
      </template>
      <template #footer>
        <Button
          icon="pi pi-times"
          label="Del"
          class="p-button-secondary"
          style="padding: 10px"
          @click="delToDo(toDo.id)"
        />
      </template>
    </Card>
  </div>
  <div v-else>No todos :)</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Button from "primevue/button";
import InputText from "primevue/inputtext";
import Card from "primevue/card";

export default defineComponent({
  name: "App",
  data() {
    return {
      toDos: [
        {
          id: 1,
          title: "Купить булок",
        },
        {
          id: 2,
          title: "Купить бумаги",
        },
        {
          id: 3,
          title: "Продать книгу",
        },
      ],
      inputValue: "",
    };
  },
  methods: {
    addToDo() {
      if (this.inputValue.trim()) {
        this.toDos.push({
          id: this.toDos.length + 1,
          title: this.inputValue,
        });
        this.inputValue = "";
      }
    },
    delToDo(id: number) {
      this.toDos = this.toDos.filter((toDo) => toDo.id != id);
    },
  },
  components: {
    Button,
    InputText,
    Card,
  },
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.p-card-body {
  display: flex;
  align-items: center;
  width: 100%;
  justify-content: space-between;
}

.p-card-footer {
  margin-bottom: 1rem;
}
</style>
