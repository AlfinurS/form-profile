<template>
  <el-dialog
    v-model="isShowModal"
    class="modal-default"
    :show-close="false"
    top="40px"
    width="auto"
    style="max-width: 728px !important"
  >
    <template #header>
      <div class="modal__wrapper">
        <div class="modal__header">
          <h2 class="modal__title">
            {{ variant === "create" ? "Добавить" : "Редактировать" }}
          </h2>
          <iconClose class="modal__close link" @click="closeModal"></iconClose>
        </div>
        <el-divider class="modal__divider"></el-divider>
      </div>
    </template>

    <div class="modal__wrapper forma">
      <div class="form__section">
        <input
          v-model="form.type"
          class="contact__input"
          type="text"
          placeholder="Тип организации"
        />
        <input
          v-model="form.name"
          class="contact__input"
          type="text"
          placeholder="Название организации"
        />
        <input
          v-model="form.description"
          class="contact__input"
          placeholder="Описание"
        />
        <input
          v-model="form.logo"
          class="contact__input"
          placeholder="Логотип"
        />
      </div>
    </div>

    <template #footer>
      <div class="modal__wrapper">
        <el-divider></el-divider>
        <div class="modal__footer">
          <button @click="closeModal" class="btn btn-plain">Закрыть</button>
          <button @click="saveData" class="btn btn-primary">Сохранить</button>
        </div>
      </div>
    </template>
  </el-dialog>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import iconClose from "@/components/icons/iconClose.vue";
import { profileDataType } from "@/types/common";
import { profileDataConst } from "@/constants/common";

export default defineComponent({
  name: "ContactModal",
  components: {
    iconClose,
  },
  emits: ["saveData"],
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
  data() {
    return {
      form: profileDataConst as profileDataType,
      isShowModal: false,
    };
  },

  methods: {
    showModal() {
      this.isShowModal = true;
    },

    closeModal() {
      this.isShowModal = false;
    },

    //назначение компонента - передать родителю данные из формы
    saveData() {
      this.isShowModal = false;
      this.$emit("saveData", { data: this.form, variant: this.variant });
    },
  },

  //выставление сохраненных данных формы
  watch: {
    dataProps(newValue) {
      this.form = JSON.parse(JSON.stringify(newValue));
    },
  },

  created() {
    this.form = JSON.parse(JSON.stringify(this.dataProps));
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/style.scss";
.modal {
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;
    margin-top: 4px;
    margin-bottom: 0px;
  }
  &__title {
    font-size: 18px;
    line-height: 24px;
    font-weight: 700;
    position: absolute;
    left: 50%;
    transform: translate(-50%, 0);
    margin-top: 0px;
    margin-bottom: 0px;
  }
  &__close {
    cursor: pointer;
    margin-right: -14px;
  }
  &__divider {
    margin-top: 24px;
    margin-bottom: 0px;
  }
  &__footer {
    display: flex;
    justify-content: space-between;
  }
  &__wrapper {
    padding-left: 40px;
    padding-right: 40px;
  }
}
</style>
