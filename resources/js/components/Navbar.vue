<template>
  <nav class="mb-4">
    <template v-if="currentUser">
      <v-navigation-drawer v-model="drawer" app color="purple darken-3" class="pt-4 pb-4">
        <v-list rounded dark>
          <v-subheader class="font-italic font-weight-medium headline">{{currentUser.name}}</v-subheader>
          <v-divider></v-divider>
          <v-list-item-group v-model="item" color="white">
            <v-list-item v-for="(link,i) in links" :key="i" router :to="link.route">
              <v-list-item-icon>
                <v-icon v-text="link.icon"></v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title class="font-weight-light" v-text="link.text"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-navigation-drawer>
    </template>
    <v-app-bar app>
      <v-app-bar-nav-icon v-if="currentUser" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title class="text-uppercase white--grey">
        <span class="font-weight-light">Rnd</span>
        <span>Template</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn @click="logOut" v-if="currentUser" text color="primary">
        <span>Log Out</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>
      <template v-if="!currentUser">
        <v-btn to="/register" text color="primary">
          <span>Register</span>
          <v-icon right>ballot</v-icon>
        </v-btn>

        <v-btn to="/login" text color="primary">
          <span>Log In</span>
          <v-icon right>account_circle</v-icon>
        </v-btn>
      </template>
    </v-app-bar>
  </nav>
</template>


<script>
import { mapGetters } from "vuex";
import { mapState } from "vuex";

export default {
  name: "navbar",
  data() {
    return {
      drawer: true,
      item: "",
      links: [
        { icon: "dashboard", text: "Dashboard", route: "/dashboard" },
        {
          icon: "folder",
          text: "Requisition Slip",
          route: "/requisition-slip"
        },
        { icon: "person", text: "Profile", route: "/profile" }
      ]
    };
  },

  methods: {
    logOut() {
      this.$store.commit("logout");
      this.$router.push("/login");
    }
  },

  computed: {
    ...mapGetters(["currentUser"]),
    ...mapState(["post"])
  }
};
</script>