<template>
  <div class="home">
    <app-toolbar></app-toolbar>
    <v-carousel>
      <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
      reverse-transition="fade-transition"
      transition="fade-transition"
      ></v-carousel-item>
    </v-carousel>
    <section id="cars" class="text-center">
      <v-container>
        <h3>Book a car now</h3>
        <v-row>
          <v-col
          cols="4"
          v-for="car in cars"
          :key="car.name"
          >
          <v-card
          :loading="loading"
          class="mx-auto my-12"
          max-width="374"
          >
          <template slot="progress">
            <v-progress-linear
            color="deep-purple"
            height="10"
            indeterminate
            ></v-progress-linear>
          </template>

          <v-img
          height="250"
          v-bind:src="car.imageurl"
          ></v-img>

          <v-card-title>{{car.name}}</v-card-title>

          <v-card-text>
            <v-row
            align="center"
            class="mx-0"
            >
            <v-rating
            :value="car.rating"
            color="amber"
            dense
            half-increments
            readonly
            size="14"
            ></v-rating>

            <div class="grey--text ml-4">
              {{car.rating}}
            </div>
          </v-row>

          <div class="my-4 subtitle-1">
            RM {{car.price}}
          </div>

          <div>{{car.description}}</div>
        </v-card-text>

        <v-divider class="mx-4"></v-divider>

      <v-card-actions>
        <v-btn
        color="deep-purple lighten-2"
        text
        v-on:click="reserve(car.name)"
        >
        Reserve
      </v-btn>
    </v-card-actions>
  </v-card>
</v-col>

</v-row>
</v-container>
</section>
<app-footer></app-footer>
</div>
</template>

<script>
// Step 1 : Import AppFooter and AppToolbar
import AppFooter from './AppFooter.vue';
import AppToolbar from './AppToolbar.vue';
export default {
  name: 'AppHome',
  components: {AppFooter, AppToolbar},
  methods: {
    reserve:function(name){ 
      this.$router.push('/booking/'+name)
    }
  },
  data () {
    return {
      cars: [  
      {
        name:"Perodua Alza",
        location:"Bandar Baru Bangi",
        description:"Perodua Alza sesuai untuk 4 orang",
        price:"80 per day",
        rating:4,
        imageurl:"https://s4.paultan.org/image/2018/09/2018-Perodua-Alza-AV-facelift-1-e1536119391982.jpg"
      }, 
      {
        name:"Perodua Viva",
        location:"Kajang",
        description:"Perodua Viva Putih sesuai untuk 4 orang",
        price:"RM90 per day",
        rating:3.5,
        imageurl:"http://paultan.org/images.paultan.org/images/d18d_viva/Perodua_Viva_34_Back.jpg"
      }, 
      {
        name:"Proton Saga",
        location:"Bandar Baru Bangi",
        description:"Proton Saga edisi baru sesuai untuk 5 orang",
        price:"100 per day",
        rating:4,
        imageurl:"https://s4.paultan.org/image/2019/08/2019-Proton-Saga-1.3-Standard-AT-1.jpg"
      }, 
      {
        name:"Preve",
        location:"Semenyih",
        description:"Preve sesuai untuk 5 orang",
        price:"120 per day",
        rating:4.5,
        imageurl:"https://s3.paultan.org/image/2018/04/Proton-Preve-Refinement-2018_Ext-1.jpg"
      }
      ],

      items: [
      {
        src: 'https://images.unsplash.com/photo-1503376780353-7e6692767b70?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=2850&q=80',
      },
      {
        src: 'https://cdn.vuetifyjs.com/images/carousel/sky.jpg',
      },
      {
        src: 'https://cdn.vuetifyjs.com/images/carousel/bird.jpg',
      },
      {
        src: 'https://cdn.vuetifyjs.com/images/carousel/planet.jpg',
      },
      ],
    }
  // 2) declare appfooger and apptoolbar in components
}
}
</script>
