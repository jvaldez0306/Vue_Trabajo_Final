<template>
  <app-menu titulo="My App"></app-menu>
  <router-view/>
</template>

<script>
 import AppMenu from '@/components/AppMenu.vue';
 export default {
      name: 'app',
      data(){
        return {
        }
      },
      methods: {
        
      },
      computed: {
      },
      mounted(){
   
      },
      components: {
        AppMenu
      }
    }
</script>

<style lang="scss">

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }

  }
  .abs-center{
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh ;
      

  }
}
</style>
