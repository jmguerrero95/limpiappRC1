<template>
         <!-- TOP BAR MENU -->
      <v-app-bar   :clipped-left="$vuetify.breakpoint.lgAndUp" app>
         <v-toolbar-title>
            <v-img :src="require('@/assets/PanelUserLogo.png')"  contain height="50"></v-img>
         </v-toolbar-title>
          <v-spacer></v-spacer>
 
       <template v-if="$vuetify.breakpoint.smAndUp">
         <v-btn text v-on:click="UpdateComponent(notificationsLink)">

          <v-badge  color="green" overlap>
               <span>Notificaciones</span>
            <template v-slot:badge>
              <span v-if="layoutUserPanel.notifications > 0">{{notificacion}}</span>
              </template>
            
                  <v-icon large>mdi-alert-circle-outline</v-icon>
            
              </v-badge>
              </v-btn>

              <v-btn icon @click="salir()">
                <v-icon>mdi-exit-to-app</v-icon>
                </v-btn>

      </template>
      </v-app-bar>
      <!-- TOP BAR MENU END -->
</template>


<script>
import { mapState, mapMutations } from "vuex";
import axios from 'axios'
export default {
  computed: {
    ...mapState(["layoutUserPanel", "user", "notificacion"]),
  },
  methods: {
    salir(){
      location.href ="http://3.15.13.45:8080/login";
    },
    ...mapMutations(["UpdateComponent","notificaciones"])
  },
  data() {
    return {
      show: false,
      notificationsLink:"compactiveservices",
      tamaño_total: 0,
    };
  },
  created: function(){
    this.tipo = this.user.tipo
    if(this.tipo==3){
      const path = 'http://3.15.13.45:8000/api/v1.0/agend_full/?estado=1'
      axios.get(path).then((response)=> {
        this.notificaciones(response.data.count)
        //this.$store.commit('notificaciones', )
        console.log(this.notificaciones) 
      })
      .catch((error) => {
        console.log(error)
      })
    }
    if(this.tipo==2){
      const path = 'http://3.15.13.45:8000/api/v1.0/agend_full/?id='+id
      axios.get(path).then((response)=> {
        this.notificaciones(response.data.count)
        //this.$store.commit('notificaciones', response.data.count)
        console.log(this.notificaciones)
      })
      .catch((error) => {
        console.log(error)
      })  
    }
  }
};
</script>