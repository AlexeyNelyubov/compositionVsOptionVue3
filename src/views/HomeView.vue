<!-- <script setup>
import { shallowRef } from "vue";
import Composition from "@/components/Composition/Composition.vue";
import Option from "@/components/Option/Option.vue";

const api = shallowRef(Composition);
</script> -->

<script>
import CompositionAPI from "@/components/Composition/Composition.vue";
import OptionAPI from "@/components/Option/Option.vue";

export default {
  components: {
    CompositionAPI,
    OptionAPI,
  },
  data() {
    return {
      api: "CompositionAPI",
    };
  },
};
</script>

<template>
  <!-- <div class="index"> -->
  <header class="index__header">
    <button class="index__header-change-api" @click="api = 'CompositionAPI'">
      Composition
    </button>
    <button class="index__header-change-api" @click="api = 'OptionAPI'">
      Option
    </button>
  </header>

  <keep-alive>
    <component :is="api"></component>
  </keep-alive>
  <!-- </div> -->
</template>

<style>
.index__header {
  margin-bottom: 10vh;
  padding: 3vh;
  display: flex;
  justify-content: center;
  border-bottom: 2px solid #000;
}
.index__header-change-api {
  margin: 2vw;
  font-size: var(--font-size, 32px);
  border: none;
  background-color: #fff;
  cursor: pointer;
}
.index__header-change-api:hover {
  color: #0000ff;
}
.index__header-change-api:active {
  color: #00ff26;
}
</style>
