<template>
    <div>
        <div class="vuejs-container">
            <button @click="openModal" class="button-user">User</button>
        
            <transition name="modal">
                <div v-if="open" class="modal" @click.self="closeModal">
                <div class="modal-content">
                    <div class="modal-header">
                    <!-- <button @click="closeModal" class="btn btn-secondary">Close</button> -->
                    </div>
                    <div class="modal-body">
                        <slot />
                    </div>
                </div>
                </div>
            </transition>
        </div>
    </div>
    </template>
    
    <script>
    export default {
    data() {
        return {
        open: false
        }
    },
    methods: {
        openModal() {
        this.open = true;
        },
        closeModal() {
        this.open = false;
        },
        saveChanges() {
        // Lógica para salvar mudanças
        this.closeModal();
        }
    }
    }
    </script>
    
    <style>
    .vuejs-container {
    width: 100%;
    padding-right: 15px;
    padding-left: 15px;
    margin-right: auto;
    margin-left: auto;
    }
    @media (min-width: 576px) {
    .vuejs-container {
        max-width: 540px;
    }
    }
    @media (min-width: 768px) {
    .vuejs-container {
        max-width: 720px;
    }
    }
    @media (min-width: 992px) {
    .vuejs-container {
        max-width: 960px;
    }
    }
    @media (min-width: 1200px) {
    .vuejs-container {
        max-width: 1140px;
    }
    }
    @media (min-width: 1400px) {
    .vuejs-container {
        max-width: 1320px;
    }
    }
    
    .modal {
    position: fixed;
    z-index: 999;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.5);
    }
    
    /* .modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    max-width: 500px;
    width: 100%;
    } */
    
    .modal-header,
    .modal-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    }
    
    .modal-body {
    margin: 20px 0;
    }
    
    .btn-close {
    background: none;
    border: none;
    }
    
    .modal-enter-active,
    .modal-leave-active {
    transition: opacity 0.5s;
    }
    
    .modal-enter,
    .modal-leave-to /* .modal-leave-active in <2.1.8 */ {
    opacity: 0;
    }

    .button-user {
      display: inline-block;
      width: 8rem;
      padding: 0.625rem 1.25rem;
      font-size: 0.875rem;
      font-weight: 500;
      color: #fff;
      background-color: #3b82f6;
      border: none;
      border-radius: 0.5rem;
      cursor: pointer;
      transition: background-color 0.3s, box-shadow 0.3s;
    }
    
    </style>