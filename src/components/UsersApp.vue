<template>
  <div>
    <div class="principal">
      <h3 class="title">Users App</h3>
    </div>
    <div class="content">
      <div id="form">
        <UsersForm @addUser="addUser" />
      </div>
      <div id="table">
        <table class="users-table">
          <thead>
            <tr>
              <th>ID</th>
              <th>Nombre</th>
              <th>Edad</th>
              <th>Email</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(user, idx) in users" :key="idx">
              <td>{{ user.id }}</td>
              <td>{{ user.first_name + " " + user.last_name }}</td>
              <td>{{ user.age ? user.age : "-" }}</td>
              <td>{{ user.email }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import UsersForm from "@/components/UsersForm.vue";

export default {
  name: "UsersApp",
  components: {
    UsersForm,
  },
  data() {
    return {
      users: [],
    };
  },
  async created() {
    const url = "https://reqres.in/api/users?page=1";

    this.axios
      .get(url)
      .then((response) => {
        this.users = response.data.data;
      })
      .catch((error) => {
        console.error(error);
      })
      .finally(() => {
        console.log(this.users);
        localStorage.setItem("users", JSON.stringify(this.users));
      });
  },
  watch: {
    users(newVal) {
      localStorage.setItem("users", JSON.stringify(newVal));
    },
  },
  methods: {
    addUser(user) {
      console.log(user);
      this.users.push(user);
    },
  },
};
</script>

<style scoped>
.principal {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.title {
  font-weight: bold;
  font-size: 1.5rem;
  padding: 0;
  margin: 0;
}

.content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 1rem;
}

#form {
  order: 1;
}

#table {
  order: 2;
}

.users-table {
  width: 100%;
  border-collapse: collapse;
  font-family: sans-serif;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0px 2px 15px rgba(0, 0, 0, 0.25);
}

.users-table thead tr {
  background-color: #ff4545;
  color: #fff;
}

.users-table th {
  padding: 0.75rem 1rem;
}

.users-table td {
  color: #323232;
  padding: 10px 10px;
}

.users-table tbody tr:nth-child(even) {
  background-color: #f2f2f2;
}
.users-table tbody tr:hover {
  cursor: pointer;
  color: #ff4545;
}

@media (max-width: 768px) {
  .content {
    grid-template-columns: 1fr;
  }
  #form {
    order: 2;
  }

  #table {
    order: 1;
  }
}
</style>