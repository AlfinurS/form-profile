<template>
  <div class="list">
    <div class="contact__wrapper">{{ dataProps.type }}</div>
    <div class="contact__wrapper">{{ dataProps.name }}</div>
    <div class="contact__wrapper">{{ dataProps.description }}</div>
    <div class="contact__wrapper">{{ dataProps.logo }}</div>

    <div @click="editContact" class="button__wrapper link">
      <iconEdit></iconEdit>
    </div>
    <div @click="deleteContact" class="button__wrapper link link--red">
      <iconDelete></iconDelete>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { profileDataType } from "@/types/common";
import iconDelete from "@/components/icons/iconDelete.vue";
import iconEdit from "@/components/icons/iconEdit.vue";

export default defineComponent({
  name: "ItemContact",
  components: { iconDelete, iconEdit },
  props: {
    dataProps: {
      type: Object as PropType<profileDataType>,
      default: () => ({}),
    },
  },

  emits: ["deleteContact", "editContact"],

  data() {
    return {};
  },

  methods: {
    //назначение компонента - передать родителю свои данные и событие удаления / редактирования
    editContact() {
      this.$emit("editContact", this.dataProps);
    },

    deleteContact() {
      this.$emit("deleteContact", this.dataProps);
    },
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/style.scss";
</style>
