<template>
    <tr class="contact-row">
      <td class="contact-cell">{{ contact.id }}</td>
      <td class="contact-cell">{{ contact.name }}</td>
      <td class="contact-cell">{{ contact.email }}</td>
      <td class="contact-cell actions">
        <button class="btn btn-edit" @click="$emit('editContact', contact)">Editar</button>
        <button class="btn btn-delete" @click="$emit('deleteContact', contact.id)">Eliminar</button>
      </td>
    </tr>
  </template>
  
  <script>
  export default {
    props: {
      contact: Object,
    },
  };
  </script>
  
  <style scoped>
  .contact-row {
    background-color: #f9f9f9;
    border-bottom: 1px solid #ddd;
    transition: background-color 0.3s ease;
  }
  
  .contact-row:hover {
    background-color: #f1f1f1;
  }
  
  .contact-cell {
    padding: 10px 15px;
    text-align: left;
  }
  
  .actions {
    text-align: center;
  }
  
  .btn {
    padding: 5px 10px;
    font-size: 14px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, color 0.3s ease;
  }
  
  .btn-edit {
    background-color: #4caf50;
    color: #fff;
  }
  
  .btn-edit:hover {
    background-color: #45a049;
  }
  
  .btn-delete {
    background-color: #f44336;
    color: #fff;
    margin-left: 5px;
  }
  
  .btn-delete:hover {
    background-color: #d32f2f;
  }
  </style>
  