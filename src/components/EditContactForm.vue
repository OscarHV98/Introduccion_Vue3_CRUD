<template>
    <div class="modal">
      <form @submit.prevent="submitForm">
        <label>Nombre:</label>
        <input v-model="contact.name" required />
        <label>Correo:</label>
        <input v-model="contact.email" type="email" required />
        <label>Dirección:</label>
        <input v-model="contact.address" />
        <label>Teléfono:</label>
        <input v-model="contact.phone" />
        <label>País:</label>
        <input v-model="contact.country" />
        <label>Ciudad:</label>
        <input v-model="contact.city" />
        <button type="submit" class="save-button">Guardar</button>
        <button type="button" @click="$emit('close')" class="cancel-button">Cancelar</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      contactData: Object,
    },
    data() {
      return {
        contact: { ...this.contactData },
      };
    },
    methods: {
      submitForm() {
        this.$emit("updateContact", this.contact);
      },
    },
  };
  </script>
  
  <style>
  .modal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 400px;
    background-color: #fff;
    padding: 20px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
  }
  
  form label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
    margin-right: 200px !important;
  }
  
  form input {
    width: 100%;
    padding: 8px;
    margin-bottom: 15px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .save-button {
    background-color: #45d066;
    color: #fff;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .cancel-button {
    background-color: #dc3545;
    color: #fff;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    margin-left: 10px;
    cursor: pointer;
  }
  
  .save-button:hover {
    background-color: #269e40;
  }
  
  .cancel-button:hover {
    background-color: #c82333;
  }
  </style>
  