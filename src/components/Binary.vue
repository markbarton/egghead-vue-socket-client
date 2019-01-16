<template>
  <v-dialog v-model="dialog" max-width="500">
    <v-card>
      <v-img :src="image" aspect-ratio="3"></v-img>
      <v-card-title class="headline">Image</v-card-title>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  sockets: {
    BINARY_NOTIFICATION: function(socket_data) {
      this.image = "data:image/jpeg;base64," + socket_data.buffer;
      this.dialog = true;
    }
  },

  data: () => ({
    dialog: false,
    image: ""
  })
};
</script>
