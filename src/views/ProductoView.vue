<template>
    <div class="container">
      <h1>Lista de Productos</h1>
        <form @submit.prevent="agregarProducto()">
          <div class="input-group mb-3">
          <input type="text" class="form-control" v-model="producto.nombre" placeholder="Nuevo producto" aria-describedby="button-addon2">
          <input type="number" class="form-control" v-model="producto.precioBob" placeholder="Precio" aria-describedby="button-addon2">
          <input type="text" class="form-control" v-model="producto.categoriaId" placeholder="Categoria Id" aria-describedby="button-addon2">
          <button class="btn btn-outline-secondary" type="submit">Agregar</button>
          </div>
        </form>
        <table class="table table-striped table-bordered table-sm">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nombre de Producto</th>
              <th scope="col">Precio BOB</th>
              <th scope="col">Categoria Id</th>              
              <th scope="col">Acciones</th>              
                   
            </tr>
          </thead>
          <tbody>
            <tr v-for="(value, key) of productos" id="key">
              <th scope="row">{{ value.id }}</th>
              <td>{{ value.nombre }}</td>
              <td>{{ value.precioBob }}</td>
              <td>{{ value.categoriaId }}</td>
              <td><button type="button" class="btn btn-primary" @click="editar(value)">Editar</button>
              <button type="button" class="btn btn-danger" @click="eliminar(value)">Eliminar</button></td>
            </tr>
          </tbody>
        </table>
    </div>
</template>

 
<script>
 
    export default {
      name: 'productoView',
      data(){
        return {
          producto:{
            nombre:null,
            precioBob:"",
            categoriaId:null

          },
          productos:[

          ]

        }
      },
      methods: {
        agregarProducto(){
          this.axios({
            method: "post",
            url:"http://localhost:3333/productos",
            data:this.producto
          })
          .then((response)=>{console.log(response);
            this.producto.nombre = null,
            this.getProductos()
          })
          .catch(e=>console.log(e));
        },
        getProductos(){
          this.axios({
            method: "get",
            url:"http://localhost:3333/productos",
            data:this.producto

          })
          .then((response)=>{
            this.productos = response.data;
            console.log(response);
          })
          .catch(e=>console.log(e));
        },
        editar(item){
          this.$router.push('/productos/'+item.id+'/editar');
          console.log(item);
        },
        eliminar(item){
          this.axios.delete("http://localhost:3333/productos/"+item.id)
           .then((response)=>{console.log(response);this.getProductos();}) 
           .catch((err)=>{console.log(err)})    
        }
      },
      computed: {
      },
      mounted(){3
        this.getProductos()
       
      },
      components: {
        
      }
    }
  </script>
  
  <style>
  </style>
  