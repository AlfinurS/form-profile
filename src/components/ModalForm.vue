<template>
  <div class="contact">
    <div class="contact__wrapper">
      <input
        @change="sendData"
        v-model="form.type"
        class="contact__input"
        type="text"
        placeholder="Тип организации"
      />
    </div>
    <div class="contact__wrapper">
      <input
        @change="sendData"
        v-model="form.name"
        class="contact__input"
        type="text"
        placeholder="Название организации"
      />
    </div>
    <div class="contact__wrapper">
      <input
        @change="sendData"
        v-model="form.description"
        class="contact__input"
        placeholder="Описание"
      />
    </div>
    <div class="contact__wrapper">
      <input
        @change="sendData"
        v-model="form.logo"
        class="contact__input"
        placeholder="Логотип"
      />
    </div>
    <div @click="deleteContact" class="button__wrapper-close link">
      <iconDelete></iconDelete>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { profileDataType } from "@/types/common";
import iconDelete from "@/components/icons/iconDelete.vue";

export default defineComponent({
  name: "FormContact",
  components: { iconDelete },
  props: {
    dataProps: {
      type: Object as PropType<profileDataType>,
      default: () => ({}),
    },
    variant: {
      type: String,
      default: "create",
    },
  },

  emits: ["sendData", "deleteContact"],

  data() {
    return {
      form: {
        id: 0,
        type: "",
        name: "",
        description: "",
        logo: null,
      } as profileDataType,
    };
  },

  methods: {
    deleteContact() {
      this.$emit("deleteContact", this.form);
    },

    sendData() {
      this.$emit("sendData", this.form);
    },
  },

  watch: {
    dataProps(newValue) {
      this.form = newValue;
    },
  },

  created() {
    this.form = JSON.parse(JSON.stringify(this.dataProps));
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/style.scss";
</style>
