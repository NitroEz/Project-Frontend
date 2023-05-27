<template>
  <div>
    <div class="input-group mb-3">
      <input
        type="text"
        class="form-control"
        v-model="code"
        placeholder="Code : xxxx-xxxx-xxxx"
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
      >
        Copy
      </button>
    </div>

    <button type="button" class="btn me-2 btn-primary" @click="gencode()">
      Generate Code
    </button>
    <button type="button" class="btn btn-success" @click="sendHook()">
      Send Hook
    </button>
  </div>
</template>
<script>
import axios from "axios";
require("dotenv").config();
export default {
  data() {
    return {
      code: "",
      webhookUrl: process.env.webhookUrl,
    };
  },
  methods: {
    gencode() {
      var code = "";
      var characters =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

      for (var i = 0; i < 16; i++) {
        var randomIndex = Math.floor(Math.random() * characters.length);
        code += characters.charAt(randomIndex);
      }
      this.code = code;
    },
    sendHook() {
      const payload = {
        embeds: [
          {
            title: "Code : || " + this.code + "  ||",
            color: 54202,
          },
        ],
      };

      axios
        .post(this.webhookUrl, payload)
        .then(() => {
          console.log("Embed sent successfully");
        })
        .catch((error) => {
          console.error("Error sending embed", error);
        });
    },
  },
};
</script>
<style></style>
