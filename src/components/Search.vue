<script>
export default {
  data() {
    return {};
  },
};
</script>

<script setup>
const props = defineProps({
  searchTerm: String,
  fromList: String,
  lastNameModifiers: {
    default: () => ({}),
    "no-whitespace": () => {},
  },
});

const emit = defineEmits(["update:searchTerm", "update:fromList"]);

const emitValue = (evt) => {
  let val = evt.target.value;
  if (props.lastNameModifiers["no-whitespace"]) {
    val = val.replace(/\s/g, "");
  }
  emit("update:fromList", val);
};
</script>

<template>
  <main>
    <div class="mt-5 d-flex">
      <input
        class="form-control"
        type="text"
        :value="searchTerm || fromList"
        placeholder="Inserisci il nome del Pokémon"
        @keydown.enter="$emit('update:searchTerm', $event.target.value)"
        @input="emitValue"
      />

      <button
        class="btn btn-primary"
        @click="$emit('update:searchTerm', $event.target.value)"
      >
        Cerca
      </button>
    </div>
  </main>
</template>

<style scoped>
input {
  width: 300px;
}

.form-control {
  margin-right: 1rem;
}
</style>