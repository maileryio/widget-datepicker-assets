<template>
  <div class="ui-datepicker">
    <input type="hidden" :name="name" />
  </div>
</template>

<script>
  export default {
    name: 'ui-datepicker',
    props: {
      name: String
    }
  }
</script>
