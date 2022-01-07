<template>
  <div>
    <p>Message Component</p>
    <div>
      <form id="burger-form">
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
            <option value="coarseBread">Coarse bread</option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Choose the meat:</label>
          <select name="meat" id="meat" v-model="meat">
            <option value="">Select the meat</option>
            <option value="meat">Maminha</option>
          </select>
        </div>
        <div class="input-container">
          <label id="optionals-title" for="optionals">Select the optional contents:</label>
          <div class="checkbox-container">
            <input
              type="checkbox"
              name="optionals"
              v-model="optionals"
              value="salami"
            >
            <span>Salami</span>
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
  optional-container {
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
