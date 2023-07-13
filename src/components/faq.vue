<template>
  <v-row class="pa-10">
    <v-col cols="12" class="d-flex justify-space-between align-center">
      <h2 class="text-h4 font-weight-medium">FAQs</h2>
      <v-tooltip text="Tooltip" left>
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            color="black"
            fab
            small
            class=""
            v-bind="attrs"
            v-on="on"
            @click="addFaq"
          >
            <v-icon color="white">mdi-plus</v-icon>
          </v-btn>
        </template>
        <span>Create FAQ</span>
      </v-tooltip>
    </v-col>

    <v-col cols="12" class="d-flex justify-center align-center">
      <faqList v-if="faqList && faqList.length > 0" :faqList="faqList" @delete="openDeleteDialog = true" @edit="editFaq" />
      <h4 v-else class="text-h5 font-weight-bold">
        Add FAQ(s) by clicking on the plus button!
      </h4>
    </v-col>
    <faqModal
      ref="faqModal"
      v-model="openModal"
      @faqDetails="faqDetails"
      :faqDetails="faqObj"
      :editMode="editMode"
      @faqUpdate="updateFaqObj"
    />
    <confirmation-dialog v-model="openDeleteDialog" @delete="deleteFaq" />
  </v-row>
</template>

<script>
import faqModal from "./faqModal.vue";
import faqList from "./faqList.vue";
import { bus } from "@/main";
import ConfirmationDialog from './confirmationDialog.vue';

export default {
  components: {
    faqModal,
    faqList,
    ConfirmationDialog,
  },
  data() {
    return {
      openModal: false,
      faqList: [],
      faqObj: {},
      editMode: false,
      faqIndex: null,
      openDeleteDialog: false
      
    };
  },
  computed: {},
  methods: {
    addFaq() {
      this.openModal = true;
    },
    faqDetails(val) {
      this.editMode = false;
      this.faqObj = val;
      this.faqList.push(val);
      localStorage.setItem("faqList", JSON.stringify(this.faqList));

      bus.$emit("showToastMessage", {
        message: "FAQ Added Successfully!",
        color: "success",
      });

      this.openModal = false;
      this.$refs.faqModal.resetForm();
      this.faqObj = {};
    },
    deleteFaq(index) {
      this.openDeleteDialog = false;
      this.faqList.splice(index, 1);
      let list = JSON.parse(localStorage.getItem("faqList"));
      bus.$emit("showToastMessage", {
        message: "FAQ Deleted Successfully!",
        color: "success",
      });
      list.splice(index, 1);
      localStorage.setItem("faqList", JSON.stringify(list));
    },
    editFaq(faq) {
      this.editMode = true;
      this.openModal = true;
      this.faqObj = faq.faq;
      this.faqIndex = faq.index
    },
    updateFaqObj(val) {
      let listIndex = JSON.parse(localStorage.getItem("faqList"))
      console.log("listIndex", listIndex[this.faqIndex] = val)
    },
  },
  mounted() {
    let list = JSON.parse(localStorage.getItem("faqList"));

    if (list && list.length > 0) {
      this.faqList = list;
    }
  },
};
</script>

<style>
</style>