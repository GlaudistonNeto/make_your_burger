<template>
  <div>
    <p>Message Component</p>
    <div>
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="nome">Client Name:</label>
          <input
            type="text"
            id="name"
            name="name"
            v-model="name"
            placeholder="Digite o seu nome"
          >
        </div>
        <div class="input-container">
          <label for="bread">Choose the bread:</label>
          <select name="bread" id="bread" v-model="bread">
            <option value="">Select the bread</option>
            <option
              v-for="bread in breads"
              :key="bread.id"
              :value="bread.type">
                {{ bread.type }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Choose the meat:</label>
          <select name="meat" id="meat" v-model="meat">
            <option value="">Select the meat</option>
            <option
              v-for="meat in meats"
              :key="meat.id"
              :value="meat.type">
                {{ meat.type }}
            </option>
          </select>
        </div>
        <div id="optionals-container" class="input-container">
        <label id="optionals-title" for="optionals">
          Select the optionals:
        </label>
        <div
          class="checkbox-container"
          v-for="optional in optionalsdata"
          :key="optional.id">
          <input
            type="checkbox"
            name="optionals"
            v-model="optionals"
            :value="optional.type">
          <span>{{ optional.type }}</span>
        </div>
      </div>
          <div class="input-container">
            <input type="submit" value="Make My Burger!" class="submit-btn">
          </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BurgerForm',
  data() {
    return {
      breads: null,
      meats: null,
      optionalsdata: null,
      name: null,
      bread: null,
      meat: null,
      optionals: [],
      msg: null,
    }
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredients");
      const data =  await req.json();

      this.breads = data.breads;
      this.meats = data.meats;
      this.optionalsdata = data.optionals;
    },

    async createBurger(e) {
      e.preventDefault();
      
      const data = {
        name: this.name,
        meat: this.meat,
        bread: this.bread,
        optionals: Array.from(this.optionals),
        status: 'Requested'
      }
      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });

      const res = await req. json();

      // system message

      // clean fiels=ds
      this.name = '',
      this.bread = ''
      this.meat = ''
      this.optionals = ''
      // clean msg
    }
  },
  mounted() {
    this.getIngredients();
  }
}
</script>

<style scoped>
  #burger-form {
    max-width: 400px;
    margin: 0 auto;
  }
  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }
  input, select {
    padding: 5px 10px;
    width: 300px;
  }
  #optionals-container {
    flex-direction: row;
    flex-wrap: wrap;
  }
  #optionals-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px slid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>
