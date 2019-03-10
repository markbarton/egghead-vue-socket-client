<template>
  <v-dialog v-model="dialog" persistent max-width="500">
    <v-card>
      <v-card-title class="headline">Select what the Image is</v-card-title>
      <v-img :src="image" aspect-ratio="2"></v-img>
      <v-layout row>
        <v-flex xs5 offset-xs1>
          <v-select :items="['Dog', 'Cat', 'Bird']" v-model="answer" label="Image" required></v-select>
        </v-flex>
        <v-flex xs4 offset-xs1>
          <v-btn
            color="green darken-1"
            v-show="!callback_success"
            @click="send_response()"
          >Send Answer</v-btn>
        </v-flex>
      </v-layout>

      <v-card-actions>
        <v-alert
          :value="callback_success"
          type="success"
          icon="check_circle"
          outline
        >Server Updated with with your response.</v-alert>
        <v-spacer></v-spacer>
        <v-btn color="primary" v-show="callback_success" @click="dialog=false">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  sockets: {
    SHOW_IMAGE: function(socket_data) {
      this.image = "data:image/jpeg;base64," + socket_data.buffer;
      this.dialog = true;
      this.answer = '';
      this.callback_success = false;
    }
  },
  data: () => ({
    dialog: false,
    answer: "",
    callback_success: false,
    image: ""
  }),
  methods: {
    send_response() {
      const message_data = {};
      message_data.response = this.answer;
      this.$socket.emit("QUIZ_RESPONSE", message_data, () => {
        // Server has ack
        this.callback_success = true;
      });
    }
  }
};
</script>
