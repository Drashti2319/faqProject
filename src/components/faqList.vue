<template>
  <v-row>
    <v-col
      cols="12"
      v-if="faqList && faqList.length > 0"
      class="d-flex justify-center"
    >
      <v-expansion-panels>
        <v-expansion-panel
          v-for="(faq, i) in faqList"
          :key="i"
          class="mb-4 border"
        >
          <v-expansion-panel-header>
            <v-row class="d-flex justify-space-between">
              <v-col cols="6">
                <h2 class="text-body-1 font-weight-medium">
                  {{ faq.question }}
                </h2>
              </v-col>
              <v-col cols="6" class="d-flex justify-end">
                <v-tooltip text="Tooltip" left>
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      color="black"
                      icon
                      class=""
                      v-bind="attrs"
                      v-on="on"
                      @click="editFaq(i, faq)"
                    >
                      <v-icon color="black">mdi-pencil</v-icon>
                    </v-btn>
                  </template>
                  <span>Edit FAQ</span>
                </v-tooltip>
                <v-tooltip text="Tooltip" left>
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      color="black"
                      icon
                      class=""
                      v-bind="attrs"
                      v-on="on"
                      @click="deleteFaq(i)"
                    >
                      <v-icon color="black">mdi-delete</v-icon>
                    </v-btn>
                  </template>
                  <span>Delete FAQ</span>
                </v-tooltip>
              </v-col>
            </v-row>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <h3 class="text-body-2 font-weight-medium">
              {{ faq.answer }}
            </h3>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-col>

    <v-col cols="12" v-else> 123 </v-col>
  </v-row>
</template>

<script>
export default {
  props: {
    faqList: {
      type: Array,
    },
  },
  methods: {
    editFaq(index, faq) {
      let params;
      params = {
        index: index,
        faq: faq,
      };
      this.$emit("edit", params);
    },
    deleteFaq(index) {
      this.$emit("delete", index);
    },
  },
};
</script>

<style>
</style>