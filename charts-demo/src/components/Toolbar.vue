<template>
  <div class="window-drag">
      <v-toolbar class="nav-toolbar window-drag"
        app
        clipped-left
        fixed
        style="z-index:5;"
      >
        <!-- DROP A LOGO HERE -->
        <!-- <h1 :to="{name: 'HomePage'}" id="headerText">Chart Demo</h1> -->
        <router-link :to="{name: 'HomePage'}" class="headline nav-text">Chart Demo</router-link>
        <v-spacer></v-spacer>

        <!-- Full nav menu for larger screens -->
        <v-toolbar-items class="hidden-md-and-down">
          <v-tooltip bottom>
            <v-btn icon @click="toggleDark" slot="activator">
              <v-icon class="">lightbulb_outline</v-icon>
            </v-btn>
            <span>Toggle light/dark</span>
          </v-tooltip>
          <v-tooltip bottom>
            <v-btn icon @click.stop="" slot="activator">
              <!-- share function when available: @click="shareURL" -->
              <v-icon class="">share</v-icon>
            </v-btn>
            <span>Share</span>
          </v-tooltip>
          <v-tooltip bottom>
            <v-btn icon @click.stop="refreshScreen" slot="activator">
              <v-icon>refresh</v-icon>
            </v-btn>
            <span>Refresh</span>
          </v-tooltip>
          <v-tooltip bottom>
            <v-btn icon @click="undock" slot="activator">
              <v-icon class="">chevron_left</v-icon>
            </v-btn>
            <span>Undock</span>
          </v-tooltip>
          <v-tooltip bottom>
            <v-btn icon @click="openApp('http://localhost:8085')" slot="activator">
              <v-icon class="">arrow_up</v-icon>
            </v-btn>
            <span>Open Dashboard Sharing</span>
          </v-tooltip>

          <v-tooltip bottom>
            <v-btn icon @click="openApp('http://localhost:8082')" slot="activator">
              <v-icon class="">chat</v-icon>
            </v-btn>
            <span>Open Chat App</span>
          </v-tooltip>
          <v-tooltip bottom>
            <v-btn icon @click="openApp('http://localhost:8083')" slot="activator">
              <v-icon class="">view_compact</v-icon>
            </v-btn>
            <span>Open Live Dashboard</span>
          </v-tooltip>

          <v-tooltip bottom>
            <v-btn icon @click="showAllWindows" slot="activator">
              <v-icon class="">list</v-icon>
            </v-btn>
            <span>Show All Windows</span>
          </v-tooltip>

          <!-- <v-btn small flat @click.stop="aboutModal = true" class="navBtn">About</v-btn> -->

          <v-menu offset-y open-on-hover max-height="400px">
            <v-btn flat slot="activator" class="navBtn">Themes
              <v-icon>arrow_drop_down</v-icon>
            </v-btn>
            <v-list>
              <v-list-tile v-for="item in themes" :key="item" @click="chooseTheme(item)">
                <v-list-tile-title>{{ item }}</v-list-tile-title>
                  <v-icon :color="item.toLowerCase()">brightness_1</v-icon>
              </v-list-tile>
            </v-list>
          </v-menu>

        </v-toolbar-items>

        <!-- Collapsed nav menu for mobile -->
        <v-toolbar-items class="hidden-lg-and-up">
          <v-tooltip bottom>
            <v-btn icon @click="toggleDark" slot="activator">
              <v-icon class="">lightbulb_outline</v-icon>
            </v-btn>
            <span>Toggle light/dark</span>
          </v-tooltip>
<<<<<<< HEAD
         
=======
          <v-tooltip bottom>
            <v-btn icon @click="undock" slot="activator">
              <v-icon class="">chevron_left</v-icon>
            </v-btn>
            <span>Undock</span>
          </v-tooltip>

>>>>>>> d003a3cb400fd54559a711a24c47ba08f8f8d7e2
          <v-menu max-height="400px">
            <v-icon slot="activator">menu</v-icon>
            <v-list>
              <v-list-tile v-for="item in themes" :key="item" @click="chooseTheme(item)">
                <v-list-tile-title>{{ item }}</v-list-tile-title>
                  <v-icon :color="item.toLowerCase()">brightness_1</v-icon>
              </v-list-tile>
            </v-list>
          </v-menu>
        </v-toolbar-items>

      </v-toolbar>


    <v-card-title>
        <div class="headline" style="width:100%;">
          <span style="margin-top: 2px; float: left;">Ticket Detail</span>
          <v-icon small id="onHoverBtn" style="float:right; margin-right:0px; margin-top: 6px;" @click.stop="closeModal">close</v-icon>
      </div>
    </v-card-title>


  </div>
</template>

<script>

import { StyleTogglerMixin } from 'jscatalyst'

  export default {
    props: [

    ],
    mixins: [StyleTogglerMixin],
    data: function () {
      return {
        themes: [],
      }
    },
    mounted() {
      this.themes = this.allThemes
      if (this.$store.state.themeMod) this.chooseTheme(this.colorTheme);
    },
    computed: {
      colorTheme: function() {
        if(this.$store.state.themeMod) return this.$store.state.themeMod.colorTheme;
        return 'blue'
      },
      displayTheme: function() {
        if (this.$store.state.themeMod) return this.$store.state.themeMod.displayTheme;
        return 'light'
      },
      allThemes: function() {
        if (this.$store.state.themeMod) return this.$store.state.themeMod.allThemes;
        return ['Blue']
      }
    },
    methods: {
      refreshScreen: function(){
        location.reload();
      }
    }
  }
</script>


<style lang="stylus">
  .navBtn
    width: 50px!important

  .responsive-img
    max-height: 46px!important
    padding-top: 5px

  .nav-toolbar
    -webkit-box-shadow: 0 2px 3px rgba(17,17,17,0.1),0 0 0 1px rgba(17,17,17,0.1)
    -moz-box-shadow: 0 2px 3px rgba(17,17,17,0.1),0 0 0 1px rgba(17,17,17,0.1)
    box-shadow: 0 2px 3px rgba(17,17,17,0.1),0 0 0 1px rgba(17,17,17,0.1)

  .nav-text
    text-decoration none
    color #000

  .list__tile__title
    font-size: 12px

  i.material-icons
    color: black

  .onHoverBtn:hover
    background-color: #D3D3D3
		cursor: pointer

  #homeButton
    text-decoration: none

  #headerText
    padding-left: 10px
    font-size: 28px
    font-family: 'Roboto'
    font-weight: normal
</style>
