<template>
  <div class="alert" :class="alertColor">
    <p>{{ alertMessage }}</p>
  </div>
</template>

<script>
export default {
  name: 'Alert',

  props: {
    alertMessage: String,
    alertColor: String
  }
};
</script>

<style lang="scss" scoped>
$alert-success: #15f044;
$alert-danger: #ff0000;

.alert {
  border-radius: 6px;
  font-size: 0.9em;
  opacity: 0;
  padding: 0;
  transition: 0.4s ease;

  &.danger,
  &.success {
    padding: 0.6em;
    opacity: 1;
  }
}

.danger {
  background: $alert-danger;
  background: linear-gradient(to right, red 0%, #ffffff00 80%);
  color: white;
}
.success {
  background: $alert-success;
  background: linear-gradient(to right, #15f044 0%, #ffffff00 80%);
  color: black;
}
</style>
