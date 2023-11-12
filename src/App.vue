<!-- 
  App выступает в качестве контроллера 

-->
<template>
  <div class="app">
    <employers-tab @selectedEmployer="getSelectedEmp" :employers="employers" />
    <my-button class="addNewEmp" @click="showModal('add')"
      >Добавить нового сотрудника</my-button
    >
    <!-- для добавления нового сотрудника вызывается функция showModal, которая принимает аргументом навание мода, в котором будет запущено модальное окно. В данном случае мы вызываем модальное окно, передавай в функцию 'add', что позволит нам добавить нового сотрудника -->
    <employer-modal
      v-if="isModalActive"
      :mode="modalMode"
      :selectedEmployer="selectedEmployer"
      @closeModal="toggleModal"
      @submit="handleFormSubmit"
    />
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import EmployersTab from "@/components/views/EmployersTab.vue";
import EmployerModal from "@/components/views/EmployerModal.vue";

import employers from "@/model/employers";

export default {
  components: {
    MyButton,
    EmployersTab,
    EmployerModal,
  },
  data() {
    return {
      employers: employers,
      isModalActive: false,
      modalMode: null,
      selectedEmployer: null,
    };
  },
  methods: {
    showModal(mode, selectedEmployer = null) {
      this.isModalActive = true;
      this.modalMode = mode;
      this.selectedEmployer = selectedEmployer;
      // Функция для отображения модального окна с заданным режимом и, при необходимости, выбранным сотрудником
    },
    toggleModal() {
      this.isModalActive = !this.isModalActive;
      this.modalMode = null;
      this.selectedEmployer = null;
      // Функция для закрытия модального окна и сброса связанных с ним данных
    },
    handleFormSubmit(formData) {
      if (this.modalMode === "add") {
        this.employers.push(formData);
      } else if (this.modalMode === "edit" && this.selectedEmployer) {
        const index = this.employers.findIndex((emp) => emp.id === formData.id);
        if (index !== -1) {
          this.employers[index] = formData;
        }
      }
      this.toggleModal();
      // Обработчик события submit из модального окна, обновляет данные о сотрудниках и закрывает модальное окно
    },
    getSelectedEmp(data) {
      // Обработчик события selectedEmployer из компонента EmployersTab, вызывает showModal в режиме 'edit'
      this.showModal("edit", data);
    },
  },
};
</script>

<style scoped>
* {
  font-family: "Montserrat", sans-serif;
  box-sizing: border-box;
}
.app {
  display: flex;
  flex-direction: column;
  max-width: 1024px;
  gap: 40px;
  min-height: 100vh;
  align-items: center;
  margin: 0 auto;
}
</style>
