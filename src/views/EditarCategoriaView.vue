<template>
    <div class="container">
    <div class="abs-center">
      <form action="" @submit.prevent="editar()">
        <div class="mb-3">
          <label class=" form-label">Editar Categoria</label>
          <input type="text" class="form-control" v-model="payload.tipo" placeholder="nombre de categoria">
        </div>
        <button type="submit" class="btn btn-primary m-2">Guardar</button>
        <button class="btn btn-secondary m-2">Cancelar</button>
      </form>
    </div>
    </div>
</template>

<script>
    export default {
      name: 'editarCategoriaView',
      props:[],
      emits:[],
      data(){
        return {
          categoriaId:0,
          payload:{
            tipo:""

          }
        }
      },
      methods: {
        load(){
          this.categoriaId = this.$route.params.id;
        },
        getCategoria(){          
          this.axios.get("http://localhost:3333/categorias/"+this.categoriaId)
          .then((response)=>{this.payload = response.data})            
          .catch((err)=>console.log(err))
            
          },
          editar(){
            this.axios.patch("http://localhost:3333/categorias/"+this.categoriaId,this.payload)
            .then((response)=>{console.log(response)})
            .catch((err)=>{console.log(err)})
          },
        
        guardar(){
          this.axios({
            method: "patch",
            url: "http://localhost:3333/categorias/"+this.$route.params.id,
            data:this.categoria
          })
          .then((response)=>{
            this.$router.push("/categorias");
            console.log(response);
          })
          .catch(e=>console.log(e));

        }      
        
      },
      computed: {
      },
      mounted(){
        this.load(),
        this.getCategoria()
      },
      components: {
      }
    }
    
  </script>
  
  <style scoped>
  form{
    max-width: 400px;
  }
  </style>
  