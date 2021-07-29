<template>
  <div class="search-container navbar">
    <img src="../assets/brand.png" style="height:10%; width:10%; margin:20px; margin-top: 10px; margin-left:250px">
    <div class="searchbar">
      <form @submit.prevent="setPokemonUrl">
        <input type="text" v-model="searchvalue">
      </form>
      <i class="fas fa-search" @click="setPokemonUrl"></i>
    </div>
  </div>
</template>

<script>
  export default {
    props: [
      'apiUrl'
    ],
    data: () => {
      return {
        searchvalue: '',
      }
    },
    methods: {
      setPokemonUrl() {
        if(this.searchvalue !== '')
          this.$emit('setPokemonUrl', this.apiUrl + this.searchvalue);
      }
    }
  }
</script>

<style lang="scss" scoped>
i{
  background: url("../assets/pokeball.png");
  background-repeat: no-repeat;

}
.navbar{
  overflow: hidden;
  background-color: #333;
  position: fixed;
  top: 0;
  width: 100%;
}
.search-container {
  background: black;
  width: 100%;
  padding: 15px;
  height: auto;
  display: flex;

}
  .searchbar {
    position: relative;
    width: 100%;
    max-width: 400px;
    padding-bottom: 20px;
    align-items: end;
    text-align: right;
    margin-left: 435px;
    margin-top: 25px;

    input {
      border: none;
      outline: none;
      border-radius: 5px;
      padding: 10px 40px 10px 10px;
      width: calc(100% - 50px);
      font-size: 1rem;
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
    }

    i {
      position: absolute;
      top: 10px;
      right: 10px;
      font-size: 1.25rem;
      color: #0A2E50;
      cursor: pointer;
    }
  }
</style>
