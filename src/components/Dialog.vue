<template>
  <v-dialog v-model="dialog" max-width="290">
    <v-card>
      <v-card-title class="headline">Please confirm?</v-card-title>

      <v-card-text>{{notification_text}}</v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>

        <v-btn color="green darken-1" flat="flat" @click="send_response(false)">No</v-btn>

        <v-btn color="green darken-1" flat="flat" @click="send_response(true)">Yes</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  sockets: {
    DIALOG_NOTIFICATION: function(socket_data) {
      this.notification_text = socket_data;
      this.dialog = true;
    }
  },

  data: () => ({
    dialog: false,
    notification_text: ""
  }),
  methods: {
    send_response(response) {
      const message_data = {};
      message_data.response = response;
      this.$socket.emit("DIALOG_RESPONSE", message_data);
      this.dialog = false;
    }
  }
};
</script>
