<template>
    <nav class="navbar">
      <div class="navbar-container">
        <a href="/" class="navbar-logo">
          <span class="navbar-logo-text">Logo Aqui!</span>
        </a>
        <div class="navbar-menu">
          <div class="navbar-router">
          <ul>
            <li><RouterLink to="/painel" class="navbar-link">Painel</RouterLink></li>
            <li><RouterLink to="/user" class="navbar-link">User</RouterLink></li>
            <li><RouterLink to="/setting" class="navbar-link">Setting</RouterLink></li>
            <li><RouterLink to="/" class="navbar-link">Logout</RouterLink></li>
          </ul>
        </div>        
        </div>
        <div class="navbar-links" :class="{ 'navbar-links-open': menuOpen }">
          <ul>
            <li><RouterLink to="/painel" class="navbar-link">Painel</RouterLink></li>
            <li><RouterLink to="/user" class="navbar-link">User</RouterLink></li>
            <li><RouterLink to="/setting" class="navbar-link">Setting</RouterLink></li>
            <li><RouterLink to="/" class="navbar-link">Logout</RouterLink></li>
          </ul>
        </div>
        <button @click="toggleMenu" class="navbar-burger" aria-label="Toggle Menu">
          <span class="navbar-burger-line"></span>
          <span class="navbar-burger-line"></span>
          <span class="navbar-burger-line"></span>
        </button>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    data() {
      return {
        dropdownOpen: false,
        menuOpen: false
      };
    },
    methods: {
      toggleDropdown() {
        this.dropdownOpen = !this.dropdownOpen;
      },
      toggleMenu() {
        this.menuOpen = !this.menuOpen;
      }
    }
  }
  </script>
  
  <style scoped>
  .navbar-router {
    display: flex;
  }
  .navbar-router ul {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
  }
  .navbar-router {
    display: block;
    padding: 0.5rem 1rem;
    color: #2d3748;
    text-decoration: none;
    transition: background-color 0.3s ease;
  }
  
  .navbar-router-mobile {
    display: none;
  }
  /* .navbar-router:hover {
    background-color: #edf2f7;
  } */
  
  .navbar-router-mobile ul {
    display: block;
    list-style: none;
    margin: 0;
    padding: 0;
    background-color: white;
    border-top: 1px solid #e2e8f0;
  }
  .navbar-router-mobile .navbar-router {
    padding: 1rem;
  }
  
  .navbar {
    background-color: #fff;
    border-bottom: 1px solid #e2e8f0;
    padding: 1rem;
    position: fixed; /* Make the navbar fixed at the top */
    top: 0; /* Position it at the top */
    left: 0; /* Ensure it spans the full width */
    width: 100%; /* Ensure it spans the full width */
    z-index: 1000;
    transition: background-color 0.3s ease;
    font-family: sans-serif;
  }
  .navbar-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1300px;
    margin: 0 auto;
  }
  .navbar-logo {
    display: flex;
    align-items: center;
    text-decoration: none;
  }
  .navbar-logo-text {
    font-size: 1.5rem;
    font-weight: 600;
    margin-left: 0.5rem;
    color: #2d3748;
  }
  .navbar-menu {
    position: relative;
  }
  .navbar-user-button {
    background-color: #2d3748;
    border: none;
    border-radius: 50%;
    padding: 0.5rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .navbar-user-img {
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
  }
  
  
  
  .navbar-dropdown {
    position: absolute;
    right: 0;
    margin-top: 0.5rem;
    background-color: white;
    border-radius: 0.375rem;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    z-index: 10;
    transition: opacity 0.3s ease;
    opacity: 0;
    visibility: hidden;
  }
  .navbar-dropdown-header {
    padding: 0.75rem 1rem;
    border-bottom: 1px solid #e2e8f0;
    background-color: #f7fafc;
  }
  .navbar-dropdown-link {
    display: block;
    padding: 0.75rem 1rem;
    color: #4a5568;
    text-decoration: none;
    transition: background-color 0.3s ease;
  }
  .navbar-dropdown-link:hover {
    background-color: #edf2f7;
    
  }
  .navbar-links {
    display: none;
  }
  .navbar-links-open {
    display: block;
  }
  .navbar-link {
    display: block;
    padding: 0.5rem 1rem;
    color: #2d3748;
    text-decoration: none;
    transition: background-color 0.3s ease;
  }
  .navbar-link:hover {
    background-color: #edf2f7;
    border-radius: 8px;
  }
  .navbar-burger {
    display: none;
    flex-direction: column;
    justify-content: space-around;
    width: 1.5rem;
    height: 1.5rem;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
  }
  .navbar-burger-line {
    width: 100%;
    height: 0.2rem;
    background-color: #2d3748;
    transition: background-color 0.3s ease;
  }
  
  @media (min-width: 767px) {
    .navbar-links-open {
      display: none;
    }
  }
  
  @media (max-width: 768px) {
    .navbar-router {
      display: block;
    }
    .navbar-burger {
      display: flex;
    }
    .navbar-router {
      display: none;
    }
  
    .navbar-links {
      display: none;
      position: absolute;
      top: 100%;
      left: 0;
      right: 0;
      background-color: white;
      border-top: 1px solid #e2e8f0;
    }
    .navbar-links-open {
      display: block;
    }
  }
  </style>
  
  
  
  