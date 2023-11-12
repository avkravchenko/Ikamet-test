<!-- Компонент отображения модального окна. Выступает в качесте вью-->

<template>
  <!-- Модальное окно для добавления нового сотрудника или редактирования существующего -->
  <div @click="closeModal" class="modal">
    <div @click.stop class="modal-content">
      <!-- Форма с полями для ввода данных о сотруднике -->
      <form @submit.prevent="handleSubmit">
        <!-- Кнопка закрытия модального окна -->
        <i @click="closeModal" class="fa-solid fa-xmark xx"></i>
        <div class="header">
          <h2>
            {{
              mode === "add" ? "Новый сотрудник" : "Редактировать сотрудника"
            }}
          </h2>
        </div>
        <!-- Группы полей для ввода данных о сотруднике -->
        <div class="form-group">
          <label for="name">Имя</label>
          <input type="text" id="name" v-model.trim="formData.name" required />
        </div>
        <div class="form-group">
          <label for="surname">Фамилия</label>
          <input
            type="text"
            id="surname"
            v-model.trim="formData.surname"
            required
          />
        </div>
        <div class="form-group">
          <label for="experience">Стаж</label>
          <input
            type="text"
            id="experience"
            v-model.trim="formData.experience"
            required
          />
        </div>
        <div class="form-group">
          <label for="age">Возраст</label>
          <input
            type="number"
            min="0"
            id="age"
            v-model="formData.age"
            required
          />
        </div>
        <div class="form-group">
          <label for="address">Адрес</label>
          <input
            type="text"
            id="address"
            v-model.trim="formData.address"
            required
          />
        </div>
        <!-- Кнопка для отправки формы -->
        <my-button class="my-button">{{
          mode === "add" ? "Готово" : "Сохранить"
        }}</my-button>
      </form>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";

export default {
  name: "EmployerModal",
  components: {
    MyButton,
  },
  props: {
    mode: {
      type: String,
    },
    selectedEmployer: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      // Данные для формы
      formData: {
        id: this.mode === "add" ? null : this.selectedEmployer?.id,
        name: this.mode === "add" ? "" : this.selectedEmployer?.name,
        surname: this.mode === "add" ? "" : this.selectedEmployer?.surname,
        experience:
          this.mode === "add" ? "" : this.selectedEmployer?.experience,
        age: this.mode === "add" ? null : this.selectedEmployer?.age,
        address: this.mode === "add" ? "" : this.selectedEmployer?.address,
      },
    };
  },
  methods: {
    // Закрытие модального окна
    closeModal() {
      this.$emit("closeModal");
    },
    // Обработка отправки формы
    handleSubmit() {
      if (this.mode === "add") {
        this.formData.id = Date.now();
      }
      // Эмиттирование события submit с данными формы и закрытие модального окна
      this.$emit("submit", this.formData);
      this.closeModal();
    },
  },
};
</script>

<style>
.modal {
  display: block;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
  padding-top: 60px;
}

.modal-content {
  position: relative;
  background-color: #fefefe;
  margin: 5% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 40%;
  border-radius: 5px;
}

.header {
  text-align: center;
}

.form-group {
  margin-bottom: 10px;
}

label {
  display: block;
  font-size: 1em;
  color: #333;
  margin-bottom: 5px;
}

input[type="text"],
input[type="number"] {
  width: 100%;
  padding: 5px;
  font-size: 1em;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-sizing: border-box;
}

.xx {
  margin-left: 95%;
  cursor: pointer;
}
</style>
