<template>
  <div>
    <p>This is detail page</p>
    <p>{{sendData}}</p>
    <p>{{city}}</p>
    <p>{{returnDate}}</p>
  </div>
</template>

<script>
export default {
  name: 'Detail',
  //mounted function is what you want to put it when the page is loading
  //Normally do some initialization for example : call the API
  mounted:function(){
    alert('When page is loaded do something')
  },
  data(){
    return{
      sendData:this.$route.params.sendDate,
      returnDate:this.$route.params.returnDate,
      city:this.$route.params.city
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-black {
  background-color: black;
}
</style>
