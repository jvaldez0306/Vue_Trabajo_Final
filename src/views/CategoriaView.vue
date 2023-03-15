<template>
    <div class="container">
      <h1>Lista de Categorias</h1>
        <form @submit.prevent="agregarCategoria()">
          <div class="input-group mb-3">
          <input type="text" class="form-control" v-model="categoria.tipo" placeholder="Nueva categoria" aria-describedby="button-addon2">
            <button class="btn btn-outline-secondary" type="submit">Agregar</button>
          </div>
        </form>
        <table class="table table-striped table-bordered table-sm">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">tipo</th>            
              <th scope="col">Acciones</th>              
            </tr>
          </thead>
          <tbody>
            <tr v-for="(value, key) of categorias" id="key">
              <th scope="row">{{ value.id }}</th>
              <td>{{ value.tipo }}</td>
              <td><button type="button" class="btn btn-primary" @click="editar(value)">Editar</button>
              <button type="button" class="btn btn-danger" @click="eliminar(value)">Eliminar</button></td>
            </tr>
          </tbody>
        </table>
    </div>
</template>

 
<script>
 
    export default {
      name: 'categoriaView',
      data(){
        return {
          categoria:{
            tipo:null
          },
          categorias:[

          ]

        }
      },
      methods: {
        agregarCategoria(){
          this.axios({
            method: "post",
            url:"http://localhost:3333/categorias",
            data:this.categoria
          })
          .then((response)=>{console.log(response);
            this.categoria.tipo = null,
            this.getCategorias()
          })
          .catch(e=>console.log(e));
        },
        getCategorias(){
          this.axios({
            method: "get",
            url:"http://localhost:3333/categorias",
            data:this.categoria

          })
          .then((response)=>{
            this.categorias = response.data;
            console.log(response);
          })
          .catch(e=>console.log(e));
        },
        editar(item){
          this.$router.push('/categorias/'+item.id+'/editar');
          console.log(item);
        },
        eliminar(item){
          this.axios.delete("http://localhost:3333/categorias/"+item.id)
           .then((response)=>{console.log(response);this.getCategorias();}) 
           .catch((err)=>{console.log(err)})    
        }
      },
      computed: {
      },
      mounted(){3
        this.getCategorias()
       
      },
      components: {
        
      }
    }
  </script>
  
  <style>
  </style>
  