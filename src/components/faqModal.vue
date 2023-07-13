<template>
  <v-dialog v-model="openDialog" width="50vw">
    <v-card rounded-lg>
      <v-card-title>
        <v-row class="d-flex justify-space-between align-center">
          <v-col cols="6">
            <h2 class="text-h5 font-weight-medium">{{editMode ? 'EDIT FAQ':'ADD FAQ'}}</h2>
          </v-col>
          <v-col cols="6" class="d-flex justify-end">
            <v-icon @click="openDialog = false" color="black">
              mdi-close
            </v-icon>
          </v-col>
        </v-row>
      </v-card-title>
      <v-divider></v-divider>
      <v-card-text>
        <v-form v-model="isValid" ref="faqForm" :key="formCount">
          <v-row class="pa-0 ma-0 pt-5">
            <v-col cols="12" class="pa-1">
              <v-text-field
                v-model="faqDetails.question"
                outlined
                dense
                label="Question*"
                required
                :rules="[(v) => !!v || 'Question is required']"
              >
              </v-text-field>
            </v-col>
            <v-col cols="12" class="pa-1">
              <v-text-field
                v-model="faqDetails.answer"
                outlined
                dense
                label="Answer*"
                required
                :rules="[(v) => !!v || 'Answer is required']"
              >
              </v-text-field>
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions class="d-flex justify-end align-center">
        <v-btn @click="resetForm" v-if="!editMode"> Reset </v-btn>
        <v-btn @click="addFaq" :disabled="!isValid" v-if="!editMode" class="black white--text"> Submit </v-btn>
        <v-btn @click="updateFaq" v-if="editMode" class="black white--text">Update</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    value: Boolean,
    faqDetails: {
      type: Object,
      default: () => {}
    },
    editMode: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      faqs: [],
      isValid: true,
      formCount: 0,
    };
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
  methods: {
    addFaq() {
      let details = { ...this.faqDetails };
      this.$emit("faqDetails", details);
    },
    resetForm() {
      this.$refs.faqForm.reset();
      this.$refs.faqForm.resetValidation();
    },
    updateFaq() {
      console.log("updateFaq")
      let updateDetails = {...this.faqDetails};
      console.log("updateeeee", updateDetails)
      this.$emit("faqUpdate", updateDetails)
    }
  },
};
</script>

<style>
</style>