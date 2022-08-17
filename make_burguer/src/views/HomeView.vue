<template>
<div>
  <banner />
  <div class="main-container">
    <h1>Make your burguer</h1>
    <BurgerForm />
  </div>
</div>
  
</template>
<script>
import banner from "../components/banner.vue"
import BurgerForm from "../components/BurgerForm.vue"
export default {
  name:"Home",
  components:{
    banner,
    BurgerForm

  }
  
}
</script>



