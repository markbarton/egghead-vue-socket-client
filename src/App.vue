<template>
  <v-app>
    <v-toolbar dark fixed app>
      <v-icon>speaker_phone</v-icon>
      <v-toolbar-title>Power Vuejs using Socket.io</v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container fluid>
        <v-layout row mb-4>
          <v-flex>
            <Graph></Graph>
          </v-flex>
        </v-layout>
        <v-layout row mb-4>
          <v-flex class="mx-1">
            <User></User>
          </v-flex>
          <v-flex>
            <Message></Message>
          </v-flex>
        </v-layout>
        <v-layout row mb-4></v-layout>
      </v-container>
    </v-content>
    <v-footer dark></v-footer>
    <Snackbar></Snackbar>
    <Dialog></Dialog>
    <Binary></Binary>
  </v-app>
</template>

<script>
import Graph from "@/components/Graph";
import User from "@/components/User";
import Message from "@/components/Message";
import Snackbar from "@/components/Snackbar";
import Dialog from "@/components/Dialog";
import Binary from "@/components/Binary";

export default {
  components: {
    Graph,
    User,
    Message,
    Snackbar,
    Dialog,
    Binary
  },
  data: () => ({
    name: "",
    group: ""
  })
};
</script>
