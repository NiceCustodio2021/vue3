<template>
 <Navbar :logo="logo_src" :alt="app_name" />
 <router-view />
 <footerComponent />
  
</template>

<script>
import Navbar from './components/Navbar.vue';
import footerComponent from './components/footerComponent.vue';


export default{
  components:{
    Navbar,
    footerComponent

    
  },
  data(){
    return{
      logo_src:"/img/logo.png",
      app_name:"Make your Burguer"
    }
  }


}
</script>
<style>
*{
  font-family: helvetica;
  padding:0;
  margin:0;
  box-sizing: border-box;
}
.main-container{
  margin:50px;
  min-height: 250px;
}
h1{
  text-align:center;
  font-size:42px;
  margin-bottom: 30px;
  color:#222;
}

</style>
