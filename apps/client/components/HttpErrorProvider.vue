<template>
  <slot></slot>
</template>

<script setup lang="ts">
import { injectHttpStatusErrorHandler } from "~/api/http.js";
import Message from "~/components/main/Message/useMessage";
import { signIn } from "~/services/auth";

useHttpStatusError();

function useHttpStatusError() {
  injectHttpStatusErrorHandler(async (errMessage, statusCode) => {
    switch (statusCode) {
      case 401:
        Message.error(errMessage, {
          duration: 2000,
          onLeave() {
            signIn(window.location.pathname);
          },
        });
      default:
        Message.error(errMessage);
        break;
    }
  });
}
</script>

<style scoped></style>
~/store/user
