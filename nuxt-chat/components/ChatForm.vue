<template>
  <v-flex sc12>
    <v-text-field
      label="Введите сообщение"
      outline
      v-model="text"
      @keydown.enter="send"
    />
  </v-flex>
</template>
<script>
export default {
  data: () => ({
    text: "",
  }),
  methods: {
    send() {
      console.log(this.text)
      this.$socket.emit(
        "createMessage",
        {
          text: this.text,
          id: this.$store.state.user.id,
        },
        (data) => {
          if (typeof data === "string") {
            console.log(data);
          } else {
             this.text = "";
          }
        }
      );
    },
  },
};
</script>
