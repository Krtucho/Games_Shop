<template>
  <div >
    <q-layout view="lHh lpr lFf"  class="shadow-2 rounded-borders">
      <q-header elevated>
        <q-toolbar>
          <q-btn flat round dense icon="menu" class="q-mr-sm" />
          <!-- <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar> -->

          <q-toolbar-title>Catálogo de juegos</q-toolbar-title>

          <!-- <q-btn flat round dense icon="whatshot" /> -->
        </q-toolbar>
      </q-header>

      <div class="q-pa-md">
          <div class="column items-center" >
            <div class="col-12 col-md-auto" style="padding-top: 5%;">
              <div class="text-h2" style="font-weight: bold; color: #43AAFF;"> Listado de Juegos de XBOX 360</div>
            </div>
            <div class="col-12 justify-content-center">
              <q-checkbox  dark keep-color v-model="showPictures" label="Mostrar imágenes" color="cyan" />
            </div>
            <div class="col-12">
              <form class="form-inline" v-on:submit.prevent="buscarCoctel()">
                <input type="text" class="form-control mr-2" placeholder="Nombre o parte del nombre del juego..." v-model="nombreCoctel"/>
                <button class="btn btn-primary">Buscar</button>
              </form>
            </div>
          </div>
        
        <div class="row justify-center" style="padding-bottom: 5%; padding-top: 1%;">
          <div class="row justify-center" style="width: 60%;"> 
            <q-list bordered separator v-for="(game, index) in getData" :key="index" class="col-12 col-sm-6 col-md-4">              
              <q-item clickable v-ripple class="column items-center"  :href="game.img">
                        <q-item-img class="col">
                          <img v-if="showPictures" img v-bind:src="game.img" alt="Generic placeholder image" width="200" class="ml-lg-5 order-1 order-lg-2" />
                        </q-item-img>
                        <q-item-label class="col"> {{ game.title }} | {{ index }}</q-item-label>
                        <q-item-label caption class="col"> {{ game.content }}</q-item-label>
                        
              </q-item>
      
            </q-list>
              <div class="column col-12 items-center">
                    <q-pagination
                          v-model="page"
                          :min="currentPage" 
                          :max="Math.ceil(gamesList.length/totalPages)"
                          :input="true"
                          input-class="text-orange-10"
                    >
                    </q-pagination>
              </div>
          </div>
        </div>
      </div>

      <q-footer elevated >
        <q-toolbar >
          <q-toolbar-title>Como contactárnos</q-toolbar-title>

          <q-space />


          <q-icon color="accent" size="2rem" style="padding-right: 1%;">
            <a href="https://t.me/VentadeJuegosCubaCanal">
              <svg xmlns="http://www.w3.org/2000/svg"  viewBox="0 0 48 48" width="48px" height="48px"><path fill="#29b6f6" d="M24 4A20 20 0 1 0 24 44A20 20 0 1 0 24 4Z"/><path fill="#fff" d="M33.95,15l-3.746,19.126c0,0-0.161,0.874-1.245,0.874c-0.576,0-0.873-0.274-0.873-0.274l-8.114-6.733 l-3.97-2.001l-5.095-1.355c0,0-0.907-0.262-0.907-1.012c0-0.625,0.933-0.923,0.933-0.923l21.316-8.468 c-0.001-0.001,0.651-0.235,1.126-0.234C33.667,14,34,14.125,34,14.5C34,14.75,33.95,15,33.95,15z"/><path fill="#b0bec5" d="M23,30.505l-3.426,3.374c0,0-0.149,0.115-0.348,0.12c-0.069,0.002-0.143-0.009-0.219-0.043 l0.964-5.965L23,30.505z"/><path fill="#cfd8dc" d="M29.897,18.196c-0.169-0.22-0.481-0.26-0.701-0.093L16,26c0,0,2.106,5.892,2.427,6.912 c0.322,1.021,0.58,1.045,0.58,1.045l0.964-5.965l9.832-9.096C30.023,18.729,30.064,18.416,29.897,18.196z"/></svg>        
            </a>
          </q-icon>

          <q-icon color="accent" size="2rem">
            <a href="https://chat.whatsapp.com/Ixc6EAtouCX59gyNnKEBvU">
              <svg xmlns="http://www.w3.org/2000/svg"  viewBox="0 0 48 48" width="48px" height="48px" fill-rule="evenodd" clip-rule="evenodd"><path fill="#fff" d="M4.868,43.303l2.694-9.835C5.9,30.59,5.026,27.324,5.027,23.979C5.032,13.514,13.548,5,24.014,5c5.079,0.002,9.845,1.979,13.43,5.566c3.584,3.588,5.558,8.356,5.556,13.428c-0.004,10.465-8.522,18.98-18.986,18.98c-0.001,0,0,0,0,0h-0.008c-3.177-0.001-6.3-0.798-9.073-2.311L4.868,43.303z"/><path fill="#fff" d="M4.868,43.803c-0.132,0-0.26-0.052-0.355-0.148c-0.125-0.127-0.174-0.312-0.127-0.483l2.639-9.636c-1.636-2.906-2.499-6.206-2.497-9.556C4.532,13.238,13.273,4.5,24.014,4.5c5.21,0.002,10.105,2.031,13.784,5.713c3.679,3.683,5.704,8.577,5.702,13.781c-0.004,10.741-8.746,19.48-19.486,19.48c-3.189-0.001-6.344-0.788-9.144-2.277l-9.875,2.589C4.953,43.798,4.911,43.803,4.868,43.803z"/><path fill="#cfd8dc" d="M24.014,5c5.079,0.002,9.845,1.979,13.43,5.566c3.584,3.588,5.558,8.356,5.556,13.428c-0.004,10.465-8.522,18.98-18.986,18.98h-0.008c-3.177-0.001-6.3-0.798-9.073-2.311L4.868,43.303l2.694-9.835C5.9,30.59,5.026,27.324,5.027,23.979C5.032,13.514,13.548,5,24.014,5 M24.014,42.974C24.014,42.974,24.014,42.974,24.014,42.974C24.014,42.974,24.014,42.974,24.014,42.974 M24.014,42.974C24.014,42.974,24.014,42.974,24.014,42.974C24.014,42.974,24.014,42.974,24.014,42.974 M24.014,4C24.014,4,24.014,4,24.014,4C12.998,4,4.032,12.962,4.027,23.979c-0.001,3.367,0.849,6.685,2.461,9.622l-2.585,9.439c-0.094,0.345,0.002,0.713,0.254,0.967c0.19,0.192,0.447,0.297,0.711,0.297c0.085,0,0.17-0.011,0.254-0.033l9.687-2.54c2.828,1.468,5.998,2.243,9.197,2.244c11.024,0,19.99-8.963,19.995-19.98c0.002-5.339-2.075-10.359-5.848-14.135C34.378,6.083,29.357,4.002,24.014,4L24.014,4z"/><path fill="#40c351" d="M35.176,12.832c-2.98-2.982-6.941-4.625-11.157-4.626c-8.704,0-15.783,7.076-15.787,15.774c-0.001,2.981,0.833,5.883,2.413,8.396l0.376,0.597l-1.595,5.821l5.973-1.566l0.577,0.342c2.422,1.438,5.2,2.198,8.032,2.199h0.006c8.698,0,15.777-7.077,15.78-15.776C39.795,19.778,38.156,15.814,35.176,12.832z"/><path fill="#fff" fill-rule="evenodd" d="M19.268,16.045c-0.355-0.79-0.729-0.806-1.068-0.82c-0.277-0.012-0.593-0.011-0.909-0.011c-0.316,0-0.83,0.119-1.265,0.594c-0.435,0.475-1.661,1.622-1.661,3.956c0,2.334,1.7,4.59,1.937,4.906c0.237,0.316,3.282,5.259,8.104,7.161c4.007,1.58,4.823,1.266,5.693,1.187c0.87-0.079,2.807-1.147,3.202-2.255c0.395-1.108,0.395-2.057,0.277-2.255c-0.119-0.198-0.435-0.316-0.909-0.554s-2.807-1.385-3.242-1.543c-0.435-0.158-0.751-0.237-1.068,0.238c-0.316,0.474-1.225,1.543-1.502,1.859c-0.277,0.317-0.554,0.357-1.028,0.119c-0.474-0.238-2.002-0.738-3.815-2.354c-1.41-1.257-2.362-2.81-2.639-3.285c-0.277-0.474-0.03-0.731,0.208-0.968c0.213-0.213,0.474-0.554,0.712-0.831c0.237-0.277,0.316-0.475,0.474-0.791c0.158-0.317,0.079-0.594-0.04-0.831C20.612,19.329,19.69,16.983,19.268,16.045z" clip-rule="evenodd"/></svg>
            </a>
          </q-icon>
        </q-toolbar>

        
        <!-- <q-btn-toggle
          v-model="model"
          flat stretch
          toggle-color="yellow"
          :options="options"
        /> -->
      </q-footer>

      <!-- <q-page-container>
        <q-page class="q-pa-md">
          <p v-for="n in 2" :key="n">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Fugit nihil praesentium molestias a adipisci, dolore vitae odit, quidem consequatur optio voluptates asperiores pariatur eos numquam rerum delectus commodi perferendis voluptate?
          </p>
        </q-page>
      </q-page-container> -->
    </q-layout>
  </div>
</template>

 <!-- <div v-if="bebidas != null">
        <div class="row">
        <div class="col-lg-8 mx-auto">
            
            <paginate  class="list-group shadow" ref="paginator" name="bebidas" :list="bebidas" :per="3">
            
            <li class="list-group-item" v-for="bebida in paginated('bebidas')" :key="bebida.idDrink">
                
                <div class="media align-items-lg-center flex-column flex-lg-row p-3" >
                <div class="media-body order-2 order-lg-1">
                    <h5 class="mt-0 font-weight-bold mb-2">{{ bebida.strDrink }}</h5>
                    <p class="font-italic text-muted mb-0 small"> {{ bebida.strCategory }} | {{ bebida.strAlcoholic }} | {{ bebida.strGlass }}</p>
                    <p>{{ bebida.strInstructions }}</p>
                </div>
                <img :src="bebida.strDrinkThumb" alt="Generic placeholder image" width="200" class="ml-lg-5 order-1 order-lg-2" />
                </div>
                
            </li>
            
            </paginate>
        
        </div>
        </div>
        <div class="d-flex justify-content-center mt-4">
            <paginate-links :classes="{ ul: 'pagination', li: 'page-item', a: 'page-link' }" for="bebidas" :show-step-links="true" :limit="2" :async="true"></paginate-links>
        </div>
    </div>
    <div v-else>
        <h2 class="display-5 text-center">Sin resultados</h2>
    </div> -->

<script>
import axios from "axios";
import { defineComponent } from 'vue';
import { ref } from 'vue'

// import VuePaginate from "vue-paginate";
// Vue.component("paginate", VuePaginate);

const linksList = [
				 {
                id: 1,
                title: "007 GoldenEye Reloaded",
                content: "1st Person Shooter",
                img: "https://m.media-amazon.com/images/I/813kZphLwCL._AC_SY500_.jpg"
            },{
                id: 2,
                title: "2006 FIFA World Cup",
                content: "1st Person Shooter",
                img: "https://m.media-amazon.com/images/I/5195746QJKL.jpg"
            },{
                id: 3,
                title: "50 Cent Blood on the Sand",
                content: "1st Person Shooter",
                img: "https://m.media-amazon.com/images/I/813kZphLwCL._AC_SY500_.jpg"
            }, {
                id: 4,
                title: "Ace Combat Assault H",
                content: "1st Person Shooter",
                img: "https://archive.org/services/img/ace-combat-assault-horizon-xbox-360-english-singapore-region/full/pct:200/0/default.jpg"
            },{
                id: 5,
                title: "Ace Combat 6",
                content: "1st Person Shooter",
                img: "https://image.jeuxvideo.com/images-sm/x3/a/c/acc6x30f.jpg"
            },{
                id: 6,
                title: "Alan Wake",
                content: "1st Person Shooter",
                img: "https://www.mobygames.com/images/covers/l/186789-alan-wake-limited-collector-s-edition-xbox-360-front-cover.jpg"
            },
            {
                id: 7,
                title: "Alone In The Dark 4",
                content: "1st Person Shooter",
                img: "https://m.media-amazon.com/images/I/51ly8UrzkzL._SY445_.jpg"
            },
            {
                id: 8,
                title: "Angry Birds Star Wars",
                content: "1st Person Shooter",
                img: "https://m.media-amazon.com/images/I/91+wY37Cj8L._SL1500_.jpg"
            },
            {
                id: 9,
                title: "Apache Air Assault",
                content: "1st Person Shooter",
                img: "https://m.media-amazon.com/images/I/91ezXgZWeOL._SY445_.jpg"
            }]

export default defineComponent({
  name: "LoginPage",
  data() {
    return {
      //bebidas: [],
      paginate: ["bebidas"],
      nombreCoctel: "",
      showPictures: ref(true),
      posts : linksList,

            gamesList: linksList,
            page: 1,
            currentPage:1,
            nextPage: null,
            totalPages: 9,
    };
  },
  methods: {
    buscarCoctel() {
      // var request = "/api/json/v1/1/search.php?s=" + this.nombreCoctel;
      // var url = "https://www.thecocktaildb.com/" + request;
      // axios.get(url).then((res) => {
      //   this.bebidas = res.data.drinks;
      //   console.log(this.bebidas);
      // });
      this.gamesList = this.posts.filter(x => x.title.toLowerCase().includes(this.nombreCoctel));
      console.log(this.gamesList);
    },
  },
  computed:{
		getData(){
			return 	this.gamesList.slice((this.page-1)*this.totalPages,(this.page-1)*this.totalPages+this.totalPages)
		}
	}
});
</script>

<style scoped>
img {
  height: 170px;
  width: 140px;
}
</style>