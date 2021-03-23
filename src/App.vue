<template>
  <v-app>
    <div class="body">
      <div class="tabs">
        <div class="tabs__tab tab1">        
          Recipe List
        </div>
        <div class="tabs__tab tab2">        
            Grocery List
        </div>
      </div>
    </div>
  </v-app>
</template>

<script>


export default {
  name: 'App',

 

  data: () => ({
    //
  }),
};
</script>

<style lang="scss">

.body {
  margin: 0 auto; 
  }

.tabs {
  justify-content: center;
  align-items: right;
  padding: 40px;
  background-color: #EAEBEA;
  &__tab {
    display: inline-block;
    padding: 8px 16px;

    border-style: solid;
    border-width: 2px;
    border-color: #6E9361;
    border-radius: 25px;
    margin-right: 10px;
    background-color: #6E9361;
    color: white;
  }
}



</style>