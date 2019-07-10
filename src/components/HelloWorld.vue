<template>
  <v-container>
    <v-layout wrap>
      <v-flex xs12 md4 sm4 mx-auto>
        <my-input></my-input>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import MyInput from './MyInput';

export default {
  components: { MyInput },
  data: () => ({})
};
</script>

<style></style>
