<template>
  <v-dialog v-model="dialog" persistent max-width="400">
    <v-card>
      <v-card-title class="headline">Please confirm?</v-card-title>

      <v-card-text>
        <v-alert
          :value="callback_success"
          type="success"
          icon="check_circle"
          outline
        >Server Updated with with your response.</v-alert>
        {{notification_text}}
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>

        <v-btn color="red darken-1" v-show="!callback_success" @click="send_response(false)">No</v-btn>
        <v-btn color="green darken-1" v-show="!callback_success" @click="send_response(true)">Yes</v-btn>
        <v-btn color="primary" flat v-show="callback_success" @click="dialog=false">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  sockets: {
    DIALOG_NOTIFICATION: function(socket_data) {
      this.notification_text = socket_data.message;
      this.dialog = true;
    }
  },

  data: () => ({
    dialog: false,
    callback_success: false,
    notification_text: ""
  }),
  methods: {
    send_response(response) {
      const message_data = {};
      message_data.response = response;
      this.$socket.emit("DIALOG_RESPONSE", message_data, () => {
        // Server has ack
        this.callback_success = true;
      });
    }
  }
};
</script>
