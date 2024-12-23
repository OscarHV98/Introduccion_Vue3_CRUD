<template>
    <div class="contact-list">
      <input
        type="text"
        v-model="filter"
        placeholder="Buscar por nombre o correo"
        class="search-bar"
      />
      <table class="contact-table">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nombre</th>
            <th>Correo</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <ContactItem
            v-for="contact in filteredContacts"
            :key="contact.id"
            :contact="contact"
            @deleteContact="deleteContact"
            @editContact="openEditModal"
          />
        </tbody>
      </table>
      <button @click="showAddModal = true" class="add-button">Agregar Contacto</button>
      <ContactForm
        v-if="showAddModal"
        @close="showAddModal = false"
        @addContact="addContact"
      />
      <EditContactForm
        v-if="showEditModal"
        :contactData="selectedContact"
        @close="closeEditModal"
        @updateContact="updateContact"
      />
    </div>
  </template>
  
  <script>
  import { contacts } from "../data/contacts";
  import ContactItem from "./ContactItem.vue";
  import ContactForm from "./ContactForm.vue";
  import EditContactForm from "./EditContactForm.vue";
  
  export default {
    components: {
      ContactItem,
      ContactForm,
      EditContactForm,
    },
    data() {
      return {
        contacts,
        filter: "",
        showAddModal: false,
        showEditModal: false,
        selectedContact: null,
      };
    },
    computed: {
      filteredContacts() {
        return this.contacts.filter(
          (c) =>
            c.name.toLowerCase().includes(this.filter.toLowerCase()) ||
            c.email.toLowerCase().includes(this.filter.toLowerCase())
        );
      },
    },
    methods: {
      deleteContact(id) {
        this.contacts = this.contacts.filter((c) => c.id !== id);
      },
      addContact(contact) {
        this.contacts.push({ ...contact, id: this.contacts.length + 1 });
      },
      openEditModal(contact) {
        this.selectedContact = { ...contact };
        this.showEditModal = true;
      },
      closeEditModal() {
        this.selectedContact = null;
        this.showEditModal = false;
      },
      updateContact(updatedContact) {
        const index = this.contacts.findIndex((c) => c.id === updatedContact.id);
        if (index !== -1) {
          this.contacts.splice(index, 1, updatedContact);
        }
        this.closeEditModal();
      },
    },
  };
  </script>
  
  <style>
  .contact-list {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }
  
  .search-bar {
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .contact-table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 20px;
  }
  
  .contact-table th,
  .contact-table td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  
  .contact-table th {
    background-color: #f4f4f4;
  }
  
  .add-button {
    padding: 10px 20px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .add-button:hover {
    background-color: #0056b3;
  }
  </style>
  