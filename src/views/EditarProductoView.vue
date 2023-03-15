<template>
    <div class="container">
    <div class="abs-center">
      <form action="" @submit.prevent="editar()">
        <div class="mb-3">
          <label class=" form-label">Editar Producto</label>
          <input type="text" class="form-control" v-model="payload.nombre" placeholder="nombre de producto">
        </div>
        <div class="mb-3">
          <input type="number" class="form-control" v-model="payload.precioBob" placeholder="precio">
        </div>
        <div>
          <input type="text" class="form-control" v-model="payload.categoriaId" placeholder="categoria">
        </div>
        <button type="submit" class="btn btn-primary m-2">Guardar</button>
        <button class="btn btn-secondary m-2">Cancelar</button>
      </form>
    </div>
    </div>
</template>

<script>
    export default {
      name: 'editarProductoView',
      props:[],
      emits:[],
      data(){
        return {
          productoId:0,
          payload:{
            nombre:"",
            precioBob:"",
            categoriaId:""
          }
        }
      },
      methods: {
        load(){
          this.productoId = this.$route.params.id;
        },
        getProducto(){          
          this.axios.get("http://localhost:3333/productos/"+this.productoId)
          .then((response)=>{this.payload = response.data})            
          .catch((err)=>console.log(err))
            
          },
          editar(){
            this.axios.patch("http://localhost:3333/productos/"+this.productoId,this.payload)
            .then((response)=>{console.log(response)})
            .catch((err)=>{console.log(err)})
          },
        
        guardar(){
          this.axios({
            method: "patch",
            url: "http://localhost:3333/productos/"+this.$route.params.id,
            data:this.producto
          })
          .then((response)=>{
            this.$router.push("/productos");
            console.log(response);
          })
          .catch(e=>console.log(e));

        }      
        
      },
      computed: {
      },
      mounted(){
        this.load(),
        this.getProducto()
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
  