<template>
  <v-app>
    <v-toolbar dark fixed app>
      <v-icon>speaker_phone</v-icon>
      <v-toolbar-title>Power Vuejs using Socket.io</v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container fluid>
        <v-layout row mb-4>
          <v-flex class="mx-1">
            <UserProfile></UserProfile>
          </v-flex>
          <v-flex>
            <ComposeMessage></ComposeMessage>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
    <v-footer dark></v-footer>
    <PopupMessage></PopupMessage>
  </v-app>
</template>

<script>
import UserProfile from "@/components/UserProfile";
import ComposeMessage from "@/components/ComposeMessage";
import PopupMessage from "@/components/PopupMessage";

export default {
  components: {
    UserProfile,
    ComposeMessage,
    PopupMessage
  }
};
</script>
