<script setup>
import { shallowRef } from "vue";
import Composition from "@/components/Composition.vue";
import Option from "@/components/Option.vue";

const api = shallowRef(Composition);
</script>

<template>
  <!-- <div class="index"> -->
  <header class="index__header">
    <button class="index__header-change-api" @click="api = Composition">
      Composition
    </button>
    <button class="index__header-change-api" @click="api = Option">
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
