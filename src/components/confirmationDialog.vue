<template>
  <v-dialog v-model="openDialog" width="40vw" persistent>
    <v-card>
      <v-card-title>
        <v-row>
          <v-col cols="12" class="d-flex justify-space-between">
            <h2 class="text-body-1 font-weight-medium">Confirm Delete?</h2>
            <v-icon color="black" @click="openDialog = false">
              mdi-close
            </v-icon>
          </v-col>
        </v-row>
      </v-card-title>
      <v-divider></v-divider>
      <v-card-text> <p class="text-body-1 pt-2 align-center">Are you sure you want to delete?</p> </v-card-text>
      <v-card-actions class="d-flex justify-end">
        <v-btn class="red white--text" @click="$emit('delete')"> Delete </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    value: Boolean,
  },
  computed: {
    openDialog: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit("input", val);
      },
    },
  },
};
</script>

<style>
</style>