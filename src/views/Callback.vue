<template>
  <div class="loading">Signing in...</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useStore } from "vuex";
import { useRouter } from "vue-router";
import { rid } from "@/rethinkid";

export default defineComponent({
  name: "Callback",
  setup() {
    const store = useStore();
    const router = useRouter();

    (async () => {
      try {
        await rid.completeLogin();
        store.dispatch("autoSignIn");
      } catch (e) {
        console.error("Sign in callback error:", e);
      }

      router.push({ name: "home" });
    })();
  },
});
</script>

<style scoped lang="scss"></style>
