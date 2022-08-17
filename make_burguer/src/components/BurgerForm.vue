<template>
<div>
  <message :msg="msg" v-show="msg" />
  <div>
      <form id="burger-form" @submit="createBurger">
          <div class="input-container">
              <label for="nome">Nom client:</label>
              <input type="text" id="nome" v-model="nome" placeholder="Write your name">

          </div>
          <div class="input-container">
              <label for="pao">Choisisez le pain:</label>
              <select name="pao" id="pao" v-model="pao">
                <option value="">Select votre pain</option>
                <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                {{pao.tipo}}</option>
              </select>
              
          </div>
          <div  id="opcionais-container" class="input-container">
              <label for="carne">Choisisez la viande:</label>
              <select name="carne" id="carne" v-model="pao">
                <option value="">Select votre viande</option>
                <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
              </select>
          </div>
          <div  id="opcionais-container" class="input-container">
              <label id="opcionais-title" for="opcionais">Choisisez les op:</label>
             <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                <span> {{opcional.tipo}} </span>

             </div>
          </div>
          
          <div class="input-container">
              <input type="submit" class="submit-btn" value="Create mon burger">
          </div>
      </form>
  </div>
</div>
  
</template>
<script>
import message from './message.vue';

export default {
    name:"BurgerForm",
    data(){
        return{
            paes:null,
            carnes:null,
            opcionaisdata:null,
            nome:null,
            pao:null,
            carne:null,
            opcionais:[],
            msg:null
        }
    },
    methods:{
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            /*console.log(data);*/
            this.paes=data.paes;
            this.carnes=data.carnes;
            this.opcionaisdata=data.opcionais;
        },
        async createBurger(e){
            e.preventDefault();
            /*console.log("Hamburguer criado")*/
            const data ={
                nome:this.nome,
                carne:this.carne,
                pao:this.pao,
                opcionais: Array.from (this.opcionais),
                status:"solicitado"
            }
           /* console.log(data);*/
           const datajson=JSON.stringify(data);
           const req= await fetch("http://localhost:3000/burgers",{
              method:"POST",
              headers:{"Content-Type": "application/json"},
              body: datajson 
           });
           const res = await req.json();
          /* console.log(res);*/
          //mensage system
          this.msg = `Pedido n° ${res.id} feito com sucesso`
          //limpar msg
          setTimeout(() => this.msg="", 3000);
          //limpar os campos
          this.nome="";
          this.carne="";
          this.pao="";
          this.opcionais="";

        }

    },
    mounted(){
        this.getIngredientes()
    },
    components: {
        message
    }

    
}
</script>
<style scoped>
  #burger-form {
    max-width: 400px;
    margin: 0 auto;
  }
  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }
  input, select {
    padding: 5px 10px;
    width: 300px;
  }
  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }
  #opcionais-title {
    width: 100%;
  }
  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }
  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }
  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }
  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>
         

