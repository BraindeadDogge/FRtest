<template>
  <v-app dark>
    <v-navigation-drawer
      fixed
      app
    >
      <nuxt-link to="/">
        <div style="padding:10px 70px">
          <v-img
            width="100%"
            src="/redcircle.png"
          ></v-img>
        </div>
      </nuxt-link>
      <v-list>
        <v-list-item-group
          v-model="selectedItem"
          color="yellow"
        >
          <v-list-item
            v-for="(item, i) in items"
            :key="i"
            :to="item.to"
            router
            exact
          >
            <v-list-item-icon>
              <v-icon x-large>{{ item.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <h4 v-text="item.title"/>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      fixed
      app
      prominent
      elevation="0"
      color="transparent"
      hide-on-scroll
      class="appbar"
    >
      <v-text-field
        label="Поиск по системе"
        outlined
        append-icon="mdi-magnify"
      ></v-text-field>
      <v-spacer />
      <v-row> 
        <v-col cols="4"></v-col>
        <v-col cols="2">
          <v-avatar
            size="65"
          >
            <img
              src="https://images.pexels.com/photos/614810/pexels-photo-614810.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
              alt="Alexander"
            >
          </v-avatar>
        </v-col>
        <v-col cols="4">
          <h4>Александр С.</h4>
          <p class="text-caption mt-1">
            Администратор
          </p>
        </v-col>
      </v-row>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      items: [
        {
          icon: 'mdi-file-document-outline',
          title: 'Опросы',
          to: '/polls'
        },
        {
          icon: 'mdi-account-multiple',
          title: 'Пользователи',
          to: '/users'
        },
        {
          icon: 'mdi-flag-variant-outline',
          title: 'Черные списки',
          to: '/blacklists'
        },
        {
          icon: 'mdi-phone',
          title: 'Колл-центр',
          to: '/callcentre'
        }
      ],
      title: 'Vuetify.js'
    }
  }
}
</script>

<style>
.appbar {
  padding: 30px;
}
</style>