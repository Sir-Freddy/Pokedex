<template>
  <div class="detail">
    <div class="detail-view" v-if="show">
      <div style="display: flex">
        <div v-if="pokemon" class="image">
          <img :src="imageUrl + pokemon.id + '.png'" alt="">
        </div>
        <div v-if="pokemon" class="image_s">
          <img :src="shinyUrl + pokemon.id + '.png'" alt="">
        </div>
      </div>
      <hr style="width:90%">
      <div v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <table class="table table-hover" style="border: 2px solid rgb(148, 148, 148); border-radius:15px; padding:10px">
          <tbody>
            <tr class="table-secondary">
              <th scope="row" style="float: left; margin-right: 20px">Exp de base</th>
              <td>{{ pokemon.base_experience }} XP</td>
            </tr>
            <tr class="table-secondary">
              <th scope="row" style="float: left; margin-right: 20px">Taille</th>
              <td>{{ pokemon.height / 10 }} m</td>
            </tr>
            <tr class="table-secondary">
              <th scope="row" style="float: left; margin-right: 20px">Poids</th>
              <td>{{ pokemon.weight / 10 }} kg</td>
            </tr>
          </tbody>
        </table>
        <h3>Types</h3>
        <div class="types">
          <div 
            v-for="(value, index) in pokemon.types"
            :key="'value'+index"
            v-bind:class="value.type.name.toLowerCase()">
            {{ value.type.name }}
          </div>
        </div>
        <h3>Capacités</h3>
        <div class="abilities">
          <div class="ability" 
            v-for="(value, index) in pokemon.abilities"
            :key="'value'+index">
            {{ value.ability.name }}
          </div>
        </div>
      </div>
      <h2 v-else>Pokemon introuvable :/</h2>
      <button class="close" @click="closeDetail">Fermer</button>
    </div>
    <i v-else class="fas fa-spinner fa-spin"></i>
  </div>
</template>

<script>
  export default {
    props: [
      'pokemonUrl',
      'imageUrl',
      'shinyUrl'
    ],
    data: () => {
      return {
        show: false,
        pokemon: {}
      }      
    },
    methods: {
      fetchData() {
        let req = new Request(this.pokemonUrl);
        fetch(req)
          .then((resp) => {
            if(resp.status === 200)
              return resp.json();
          })
          .then((data) => {
            this.pokemon = data;
            this.show = true;
          })
          .catch((error) => {
            console.log(error);
          })
      },
      closeDetail() {
        this.$emit('closeDetail');
      }
    },
    created() {
      this.fetchData();
    }
  }
</script>

<style lang="scss" scoped>
  .detail {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    position: fixed;
    top: -55px;
    left: 0;
    padding: 90px 10px 10px;
    width: calc(100% - 20px);
    height: calc(100vh - 20px);
    background: rgba($color: #000000, $alpha: .7);
    .detail-view {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      position: relative;
      width: 100%;
      max-width: 510px;
      padding: 50px 0 0;
      background-color: #fff;
      border-radius: 10px;


      h2 {
        text-transform: capitalize;
      }
      .data {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        flex-direction: column;
        width: 100%;
        margin-bottom: 40px;
        .property {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px solid #ccc;
          margin-bottom: 10px;

          .left { float: left; }
          .right { float: right; }
        }
        h3 {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px solid #ccc;
        }
        .types, .abilities {
          display: flex;
          justify-content: flex-start;
          flex-wrap: wrap;
          width: 90%;
          max-width: 400px;
  
          .type, .ability {
            margin: 0 10px 10px 0;
            padding: 5px 10px;
            border-radius: 20px;
            color: rgb(0, 0, 0);
            font-size: 1rem;
            letter-spacing: 2px;
            text-transform: capitalize;
            word-wrap: none;
            word-break: keep-all;
          }
          .ability { background-color: #ffffff; border: 2px solid rgb(148, 148, 148); }
        }
      }
      .close {
        outline: none;
        border: none;
        border-radius: 5px;
        background-color: rgb(0, 0, 0);
        color: #efefef;
        padding: 10px 20px;
        margin-bottom: 20px;
        font-size: 1.2rem;
        cursor: pointer;
      }
    }
    i {
      font-size: 2rem;
      color: #efefef;
    }
  }
.bug {
  background-color: #abb642;
  border: 3px solid #aab361;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.dark {
  background-color: #6c584a;
  border: 3px solid #796b62;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.dragon {
  background-color: #6843ef;
  border: 3px solid #8567f1;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.electric {
  background-color: #f2d054;
  border: 3px solid #ffe071;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.fairy {
  background-color: #e29dac;
  border: 3px solid #facad5;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.flying {
  background-color: #a493ea;
  border: 3px solid #cabcff;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.fighting {
  background-color: #b13c31;
  border: 3px solid #df695e;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.fire {
  background-color: #ffad73;
  border: 3px solid #e28544;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.ghost {
  background-color: #6c5a94;
  border: 3px solid #917fb8;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.grass {
  background-color: #8bc560;
  border: 3px solid #b5e093;
  margin: 0 10px 10px 0;
  padding: 5px 10px;
  border-radius: 20px;
  color: #fff;
  font-size: 1rem;
  letter-spacing: 2px;
  text-transform: capitalize;
}
.ground {
  background-color: #dbc074;
  border: 3px solid #fce3a1;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.ice {
  background-color: #a6d6d7;
  border: 3px solid #d8feff;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.normal {
  background-color: #a8a77d;
  border: 3px solid #dfdebb;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.poison {
  background-color: #94489b;
  border: 3px solid #bf7bc5;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.psychic {
  background-color: #e66388;
  border: 3px solid #f791ae;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.rock {
  background-color: #b4a04a;
  border: 3px solid #ecda8a;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.steel {
  background-color: #b8b8ce;
  border: 3px solid #9898a1;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
.water {
  background-color: #6f91e9;
  border: 3px solid #9cb8ff;
  margin: 0 10px 10px 0;
padding: 5px 10px;
border-radius: 20px;
color: #fff;
font-size: 1rem;
letter-spacing: 2px;
text-transform: capitalize;
}
</style>
