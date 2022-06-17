<template>
  <date-picker
    v-model="value"
    prefix-class="ui"
    value-type="format"
    :format="format"
    :input-class="className"
    :input-attr="{ name }"
    :type="type"
    :clearable="clearable"
    :disabled="disabled"
    :placeholder="placeholder"
    :open.sync="open"
    :hour-options="hourOptions"
    :minute-options="minuteOptions"
    :second-options="secondOptions"
    @change="handleChange">
  </date-picker>
</template>

<script>
  import DatePicker from 'vue2-datepicker';

  let parseJson = (data) => {
    try {
      return JSON.parse(data);
    } catch (e) {}
    return data;
  };

  export default {
    name: 'ui-datepicker',
    components: {
      DatePicker
    },
    props: {
      name: String,
      value: String,
      format: String,
      type: {
        type: String,
        validator(value) {
          return ['date', 'datetime', 'year', 'month', 'time', 'week'].includes(value)
        }
      },
      clearable: {
        type: Boolean,
      	default: false
      },
      disabled: {
      	type: Boolean,
      	default: false
      },
      className: String,
      placeholder: String,
      closeOnSelect: {
      	type: String,
      	default: 'second'
      },
      hourOptions: Array,
      minuteOptions: Array,
      secondOptions: Array
    },
    data() {
      return {
        value: this.value,
        open: false
      }
    },
    methods: {
      handleChange(value, type) {
        if (type === this.$props.closeOnSelect) {
          this.open = false;
        }
      }
    }
  }
</script>

<style lang="scss">
  $namespace: 'ui';
  $default-color: #555;
  $primary-color: #007bff;

  @import 'node_modules/vue2-datepicker/scss/index.scss';

  .ui-datepicker {
    width: 100%;

    .ui-icon-calendar,
    .ui-icon-clear {
      right: 17px;
      color: inherit;
    }

    .form-control {
      padding-right: 3rem;

      &.is-valid,
      &.is-invalid {
        padding-right: calc(1.5em + 0.75rem + 2rem) !important;

        & + .ui-icon-calendar,
        & + .ui-icon-clear {
          right: 40px;
        }
      }
    }
  }
</style>
