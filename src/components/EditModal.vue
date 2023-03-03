<template>
  <div class="modal" v-if="showModal">
    <div class="modal-content">
      <h2>Edit Car</h2>
      <form>
        <div>
          <label>ID:</label>
          <span>{{ car.id }}</span>
        </div>
        <div>
          <label>CARID:</label>
          <span>{{ car.carId }}</span>
        </div>
        <div>
          <label>INSTOCK:</label>
          <input type="radio" name="inStock" v-model="car.inStock" value="true" />
          <label for="inStockTrue">true</label>
          <input type="radio" name="inStock" v-model="car.inStock" value="false" />
          <label for="inStockFalse">false</label>
        </div>
        <div>
          <label>HP:</label>
          <input type="number" v-model="car.hp" min="100" max="550" @input="checkHp" />
          <div v-if="!isHPValid" class="invalid-feedback">HP değeri 100-550 arasında olmalıdır.</div>
        </div>
        <div>
          <label>PRICE:</label>
          <input type="text" v-model="car.price" @input="updatePrice" />
        </div>
        <div>
          <label>COLOR:</label>
          <input type="radio" name="color" v-model="car.color" value="red" />
          <label for="redColor">red</label>
          <input type="radio" name="color" v-model="car.color" value="blue" />
          <label for="blueColor">blue</label>
          <input type="radio" name="color" v-model="car.color" value="yellow" />
          <label for="blueColor">yellow</label>
        </div>
      </form>
      <div class="modal-buttons">
        <button @click.prevent="$emit('save')" :disabled="isDisabled" class="btn save-btn">Save</button>
        <button @click.prevent="$emit('close')" class="btn cancel-btn">Cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "EditModal",
  props: ["car", "showModal"],
  data() {
    return {
      isHPValid: true,
      isDisabled: false,
    };
  },
  methods: {
    updatePrice(event) {
      const newPrice = event.target.value
        .replace(/\D/g, "")
        .replace(/\B(?=(\d{3})+(?!\d))/g, ".");
      this.car.price = newPrice;
    },
    checkHp() {
      if (this.car.hp < 100 || this.car.hp > 550) {
        this.isHPValid = false;
        this.isDisabled = true;
      } else {
        this.isHPValid = true;
        this.isDisabled = false;
      }
    }
  }
};
</script>

<style scoped>
.modal {
  display: block;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 50%;
  margin-top: 30px;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

form > * {
  margin-bottom: 20px;
}

input[type="checkbox"] {
  margin-right: 10px;
}

.invalid-feedback {
  font-size: 12px;
  color: red;
  margin-top: 5px;
}

.modal-buttons {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.modal-buttons button {
  margin-left: 10px;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button.save-btn {
  background-color: #4caf50;
  color: white;
}

button.save-btn:disabled {
  opacity: 0.5;
}

button.cancel-btn {
  background-color: #999999;
  color: white;
}
</style>