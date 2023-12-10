<template>
  <div
  class="box type-btn d-flex justify-content-between align-items-center pe-3 ps-3"
    @click="show = !show"
  >
    <p class="m-0 d-flex align-items-center">{{ typeSelected }}</p>

  <img class="img-fluid" :src="arrowDown"/>
    
  </div>
  <div v-show="show" class="dropdown-content mt-1">
    <div
      class="dropdown-item pb-3"
      v-for="(dropdownOption, index) in options"
      :key="index"
    >
       <input class="checkbox_location form-check-input" type="checkbox" id="flexCheckDefault"   @click="onOptionClick(dropdownOption)">
       <label  class="btn mt-2 ps-0 type-option text-start" for="">{{ dropdownOption }}</label>
  
    </div>
  </div>
</template>

<script>
import arrowDown from "/src/assets/images/arrow-down.svg";

export default {
  props: {
    options: {
      type: Array,
      required: true,
    },

  },
  data() {
    return {
      arrowDown: arrowDown,
      show: false,
      typeSelected: this.options.option1,

    };
  },
  methods: {
    showDropdown() {
      this.show = !this.show;
    },
    onOptionClick(option) {
      this.typeSelected = option 
      this.show = true; // don't Hide the dropdown after selecting an option
      this.$emit('update:typeSelected', option); // Emit the updated value to the parent

                           }},};
</script>

<style scoped>
.type-btn { cursor: pointer; }

.dropdown-content {
  position: absolute; /* to make appears above other elements on the page. */
  width: 100%;
  max-width: 200px;
  border-radius: 10px;}


.dropdown-item {
  height: 50px;
  border: 1px solid var(--placeholder);
  border-radius: 5px;
  display: flex;
  margin:0px 0px 0px 500px;
  padding-left: 18px;}

.dropdown-item:first-child {
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  margin-top: 100px;
  }

.dropdown-item:last-child {
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;}

.type-option {
  color: var(--white-color);
  border: none;
  outline: none;
  width: 100%;
  font-weight: 400px;
  font-size: 16px;
  font-style: normal;
  line-height: normal;
  text-transform: capitalize;}

.box {
  border: 1px solid var(--placeholder);
  position: absolute;
  width: 200px;
  height: 60px;
  border-radius: 10px;
  color: var(--white-color);
  margin:40px 0px 0px 500px;}

  .form-check-input{
    margin: 20px 20px 0px 0px;
    background-color: var(--dark-blue-color);
    border-color: var(--second-blue-color);
    border-radius: 5px;
    width: 18px;
    height: 18px;}

.form-check-input:checked{ background-color: var(--second-blue-color); }

</style>
