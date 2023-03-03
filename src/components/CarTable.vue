<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>CARID</th>
          <th>INSTOCK</th>
          <th>HP</th>
          <th>PRICE</th>
          <th>COLOR</th>
          <th>EDIT</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(car) in cars" :key="car.id">
          <td>{{ car.id }}</td>
          <td>{{ car.carId }}</td>
          <td>
            <div v-if="!editing || (editing && car.id !== editCar.id)">{{ car.inStock }}</div>
            <div v-else>
              <label>
                <input type="radio" v-model="editCar.inStock" value="true" />
                True
              </label>
              <label>
                <input type="radio" v-model="editCar.inStock" value="false" />
                False
              </label>
            </div>
          </td>
          <td>{{ car.hp }}</td>
          <td>{{ car.price.toLocaleString('tr-TR') || '-' }} €</td>
          <td>
            {{ car.color }}
            <span class="color-indicator" :style="{ backgroundColor: car.color }"></span>
          </td>
          <td>
            <button @click="openModal(car)">Edit</button>
          </td>
        </tr>
      </tbody>
    </table>

    <EditModal :car="selectedCar" :show-modal="showModal" @save="saveCar" @close="closeModal" />
  </div>
</template>

<script>
import EditModal from "@/components/EditModal.vue";

export default {
  name: "CarTable",
  components: {
    EditModal
  },

  data() {
    return {
      cars: [
        {
          id: 1,
          carId: "HJKFSHJK42525fsdfs",
          inStock: true,
          hp: 200,
          price: 10000,
          color: "red"
        },
        {
          id: 2,
          carId: "HFJKAHAK6872431",
          inStock: false,
          hp: 300,
          price: 15000,
          color: "blue"
        },
        {
          id: 3,
          carId: "HFJKAHAK6872432",
          inStock: true,
          hp: 400,
          price: 20000,
          color: "yellow"
        }
      ],
      selectedCar: null,
      showModal: false,
      editCar: {
        id: null,
        carId: null,
        inStock: null,
        hp: null,
        price: null,
        color: null
      },
      editing: false,
      originalData: {}
    };
  },
created() {
  this.originalData = JSON.parse(JSON.stringify(this.cars));
  console.log('created', this.originalData)
},
  methods: {
    openModal(car) {
      this.selectedCar = car;
      this.showModal = true;
    },

    closeModal() {
      this.selectedCar = null;
      this.showModal = false;
      this.cars = this.originalData;
      console.log('cars', this.cars)
    },

    saveCar() {
      this.closeModal();
    }
  }
};
</script>

<style scoped>
table {
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid black;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #ddd;
}

.color-indicator {
  display: inline-block;
  width: 90px;
  height: 10px;
  margin-left: 5px;
}
</style>
