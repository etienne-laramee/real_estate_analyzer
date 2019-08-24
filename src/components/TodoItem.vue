<template>
  <div class="todo-item">
    <p><i>{{entry.MlsNumber}}</i></p>
    <p>{{entry.Property.Address.AddressText}}</p>
    <p><b>{{entry.Property.Price}}</b></p>
    <p>{{entry.PublicRemarks}}</p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["entry"],
  methods: {}
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>