<template>
    <div>
        <div class="vuejs-container">
            <h1>User</h1>
            <br>
            <ModalUser>
                <form class="form-container" @submit.prevent="submitForm">
                    <h2>{{ isEditing ? 'Update' : 'Create User' }}</h2><br>
                    <div v-if="status" :class="{'success': success, 'error': !success}">
                    {{ status }}
                    </div><br>
                    <div>
                        <div class="form-group">
                        <label for="username">Username</label>
                        <input id="username" v-model="name" type="text" class="form-input">
                        </div>
                    </div>
                    <div>
                        <div class="form-group">
                        <label for="email">Email</label>
                        <input id="email" v-model="email" type="email" class="form-input">
                        </div>
                    </div>
                    <div>
                        <div class="form-group">
                            <label for="password">Password</label>
                            <input id="password" v-model="password" type="password" class="form-input">
                        </div> 
                    </div>
                    <button type="submit" class="form-button">{{ isEditing ? 'Update' : 'Create User' }}</button>
                </form>
            </ModalUser>
            <br>
            <div class="table-container">
            <table>
              <thead>
                <tr>
                  <th scope="col">Username</th>
                  <th scope="col">Email</th>
                  <th scope="col">Edit</th>
                  <th scope="col">Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="user in users" :key="user.id">
                  <td>{{ user.name }}</td>
                  <td>{{ user.email }}</td>
                  <td><button class="btn-edit" @click="loadUser(user.id)">Edit</button></td>
                  <td><button class="btn-delete" @click="deleteUser(user.id)">Delete</button></td>
                </tr>
              </tbody>
            </table>
            <br><br><br><br><br><br>
          </div>
        </div>
    </div>
</template>

<script>
  export default {
    middleware: 'auth',
    data() {
      return {
        name: '',
        email: '',
        password: '',
        status: '',
        success: false,
        users: [],
        isEditing: false,
        currentUserId: null
      };
    },
    methods: {
      register() {
        const options = {
          method: 'POST',
          headers: {
            Authorization: 'Bearer xau_VXR7bwVEySeLTMjgHQEEb4kVwXtwrpvv0',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            name: this.name,
            email: this.email,
            password: this.password
          })
        };
  
        fetch('https://app-developer-s-workspace-6anock.us-east-1.xata.sh/db/database-cloud:main/tables/user/data?columns=id', options)
          .then(response => response.json())
          .then(response => {
            if (response.id) {
              this.status = 'Successfully registered!';
              this.success = true;
              this.fetchUsers();
              this.resetForm();
            } else {
              this.status = 'Registration failed. Please try again.';
              this.success = false;
            }
          })
          .catch(err => {
            this.status = 'An error occurred. Please try again.';
            this.success = false;
          });
      },
      fetchUsers() {
        const options = {
          method: 'POST',
          headers: {
            Authorization: 'Bearer xau_VXR7bwVEySeLTMjgHQEEb4kVwXtwrpvv0',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            columns: ["name", "email", "password"],
            page: { size: 15 }
          })
        };
  
        fetch('https://app-developer-s-workspace-6anock.us-east-1.xata.sh/db/database-cloud:main/tables/user/query', options)
          .then(response => response.json())
          .then(response => {
            this.users = response.records;
          })
          .catch(err => {
            console.error(err);
          });
      },
      loadUser(userId) {
        const user = this.users.find(user => user.id === userId);
        if (user) {
          this.name = user.name;
          this.email = user.email;
          this.password = user.password;
          this.currentUserId = userId;
          this.isEditing = true;
        }
      },
      updateUser() {
        const options = {
          method: 'PATCH',
          headers: {
            Authorization: 'Bearer xau_VXR7bwVEySeLTMjgHQEEb4kVwXtwrpvv0',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            name: this.name,
            email: this.email,
            password: this.password
          })
        };
  
        fetch(`https://app-developer-s-workspace-6anock.us-east-1.xata.sh/db/database-cloud:main/tables/user/data/${this.currentUserId}?columns=id`, options)
          .then(response => response.json())
          .then(response => {
            if (response.id) {
              this.status = 'Successfully updated!';
              this.success = true;
              this.fetchUsers();
              this.resetForm();
            } else {
              this.status = 'Update failed. Please try again.';
              this.success = false;
            }
          })
          .catch(err => {
            this.status = 'An error occurred. Please try again.';
            this.success = false;
          });
      },
      deleteUser(userId) {
        const options = {
          method: 'DELETE',
          headers: {
            Authorization: 'Bearer xau_VXR7bwVEySeLTMjgHQEEb4kVwXtwrpvv0',
            'Content-Type': 'application/json'
          }
        };
  
        fetch(`https://app-developer-s-workspace-6anock.us-east-1.xata.sh/db/database-cloud:main/tables/user/data/${userId}?columns=id`, options)
          .then(response => response.json())
          .then(response => {
            if (response.id) {
              this.status = 'Successfully deleted!';
              this.success = true;
              this.fetchUsers();
            } else {
              this.status = 'Deletion failed. Please try again.';
              this.success = false;
            }
          })
          .catch(err => {
            this.status = 'An error occurred. Please try again.';
            this.success = false;
          });
      },
      submitForm() {
        if (this.isEditing) {
          this.updateUser();
        } else {
          this.register();
        }
      },
      resetForm() {
        this.name = '';
        this.email = '';
        this.password = '';
        this.currentUserId = null;
        this.isEditing = false;
      }
    },
    mounted() {
      this.fetchUsers();
    }
  };
</script>

<style>
body {
    background-color: #f1f4f9;
}

.form-container {
    font-size: 16px;
    padding: 50px;
}

.table-container {
    overflow-x: auto;
    border-radius: 10px;
}

table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.875rem;
    text-align: left;
    color: #6b7280;
    font-size: 18px;
    font-family: sans-serif;
    
}

thead {
    background-color: #e6eefd;
    text-transform: uppercase;
    color: #4b5563;
   
}

th, td {
    padding: 0.75rem 1.5rem;
}

th {
    font-size: 0.75rem;
    font-weight: 600;
}

tbody tr {
    background-color: #fff;
    border-bottom: 1px solid #e5e7eb;
    
}

tbody tr:nth-child(even) {
    background-color: #f9fafb;
   
}

tbody tr:last-child {
    border-bottom: none;
}

tbody th {
    font-weight: 500;
    color: #111827;
    white-space: nowrap;
}

.btn-edit {
    display: inline-block;
    width: 4rem;
    padding: 0.625rem 1.25rem;
    font-size: 0.875rem;
    font-weight: 500;
    color: #fff;
    background-color: #007732;
    border: none;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: background-color 0.3s, box-shadow 0.3s;
}

.btn-delete {
    display: inline-block;
    padding: 0.625rem 1.25rem;
    font-size: 0.875rem;
    font-weight: 500;
    color: #fff;
    background-color: #a30000;
    border: none;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: background-color 0.3s, box-shadow 0.3s;
}
</style>