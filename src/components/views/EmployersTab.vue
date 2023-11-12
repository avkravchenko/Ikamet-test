<!-- Компонент отображения таблицы сотрудников. Выступает в качесте вью-->
<template>
  <div>
    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th>Имя</th>
            <th>Фамилия</th>
            <th>Стаж</th>
            <th>Возраст</th>
            <th>Адрес</th>
            <th>Действие</th>
          </tr>
        </thead>
        <tbody>
          <!-- Используется директива v-for для отображения данных о каждом сотруднике из массива employers -->
          <tr v-for="employer in employers" :key="employer.id">
            <td>{{ employer.name }}</td>
            <td>{{ employer.surname }}</td>
            <td>{{ employer.experience }}</td>
            <td>{{ employer.age }}</td>
            <td>{{ employer.address }}</td>
            <td>
              <!-- Кнопка для вызова функции editEmployer при редактировании сотрудника -->
              <button @click="editEmployer(employer)" class="edit-button">
                <i class="fas fa-edit"></i>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    employers: {
      type: Array,
      required: true,
    },
  },
  methods: {
    // Метод для эмиттирования события selectedEmployer с выбранным сотрудником
    editEmployer(employer) {
      this.$emit("selectedEmployer", employer);
    },
  },
};
</script>

<style lang="scss" scoped>
.table-container {
  overflow-x: auto;

  table {
    background-color: #f4f4f4;
    border-collapse: collapse;
    width: 100%;
    margin-top: 50px;
    border-radius: 10px;

    th,
    td {
      font-weight: 300;
      text-align: left;
    }

    td {
      padding: 5px 10px;
    }

    th {
      background-color: #4caf50;
      color: white;
      padding: 9px 10px;

      &:first-child {
        border-radius: 10px 0 0 0;
      }

      &:last-child {
        border-radius: 0 10px 0 0;
      }
    }

    tr:nth-child(even) {
      background-color: #f2f2f2;
    }

    tr:hover {
      background-color: #ddd;
    }

    .edit-button {
      background-color: #008cba;
      color: white;
      border: none;
      padding: 8px 12px;
      font-size: 10px;
      cursor: pointer;
      border-radius: 5px;

      &:hover {
        background-color: #005f6b;
      }
    }

    @media (max-width: 768px) {
      th,
      td {
        font-size: 12px;
        padding: 8px;
      }
    }

    @media (max-width: 503px) {
      th,
      td {
        font-size: 10px;
        padding: 6px;
      }
    }
  }
}
</style>
