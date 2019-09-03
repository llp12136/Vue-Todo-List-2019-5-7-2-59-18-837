<template>
  <div id="forms">
    <input type="text" :value="inputingText" @change="handlechange"/>
    <button @click="handleAdd">Add</button>
  </div>
</template>
<script>
export default {
  name: "forms",
  data: function() {
    return {
      inputingText: ""
    };
  },
  methods: {
    handleAdd: function() {
      this.$emit("addNewToDo", this.inputingText);
      this.inputtingText = "";
    },
    handlechange:function(event){
      this.inputingText=event.target.value

}
  }
};
</script>