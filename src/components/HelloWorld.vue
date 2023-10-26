<template>
  <div class="container">
    <header class="header">
      <h1 class="title">UITEC App</h1>
      
    </header>
    <main>
      <div class="table-container">
        <p>Creado por <a href="">Andres MORETA</a> 2023</p>
        <h2>Equipos</h2>
        <table class="table">
          <thead>
            <tr>
              <th>Nombres</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Computadora</td>
            </tr>
            <tr>
              <td>Arduino</td>
            </tr>
            <tr>
              <td>Router</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="table-container">
        <h2>Estudiantes</h2>
        <table class="table">
          <thead>
            <tr>
              <th>Nombre</th>
              <th>Equipo</th>
              <th>Estado</th>
              <th>Fecha Adquisición</th>
              <th>Fecha Máxima</th>
              <th>Fecha Devuelto</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(usuario, index) in usuarios" :key="index">
              <td>{{ usuario.nombre }}</td>
              <td>{{ usuario.equipo }}</td>
              <td :class="usuario.estado">{{ usuario.estado }}</td>
              <td>{{ usuario.fechaAdquisicion }}</td>
              <td>{{ usuario.fechaMaxima }}</td>
              <td>{{ usuario.fechaDevuelto }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="table-container">
        <h2>Pagos Pendientes</h2>
        <table class="table">
          <thead>
            <tr>
              <th>Estudiante</th>
              <th>Equipo</th>
              <th>Total a Pagar</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(usuario, index) in usuarios" :key="index">
              <td>{{ usuario.nombre }}</td>
              <td>{{ usuario.equipo }}</td>
              <td>$ {{ usuario.deuda }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </main>
    <footer>
     
    </footer>
    <div class="input-form">
      <h2>Add a Student</h2>
      <form @submit.prevent="addStudent">
        <label for="nombre">Nombre:</label>
        <input type="text" v-model="newStudent.nombre" required><br><br>
        <label for="equipo">Equipo:</label>
        <input type="text" v-model="newStudent.equipo" required><br><br>
        <label for="estado">Estado:</label>
        <input type="text" v-model="newStudent.estado" required><br><br>
        <label for="fechaAdquisicion">Fecha Adquisición:</label>
        <input type="text" v-model="newStudent.fechaAdquisicion" required><br><br>
        <label for="fechaMaxima">Fecha Máxima:</label>
        <input type="text" v-model="newStudent.fechaMaxima" required><br><br>
        <label for="fechaDevuelto">Fecha Devuelto:</label>
        <input type="text" v-model="newStudent.fechaDevuelto" required><br><br>
        <button type="submit" class="add-button">Add Student</button><br><br>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeVue",
  data() {
    return {
      usuarios: [
        // Your existing data
      ],
      newStudent: {
        nombre: "",
        equipo: "",
        estado: "",
        fechaAdquisicion: "",
        fechaMaxima: "",
        fechaDevuelto: "",
        deuda: 0,
      },
    };
  },
  methods: {
    CalcularDeuda() {
      // Your existing method
    },
    addStudent() {
      // Calculate deuda for the new student and push them to the usuarios array
      const fecha = new Date(this.newStudent.fechaMaxima);
      const fechaDevuelto = new Date(this.newStudent.fechaDevuelto);
      this.newStudent.deuda = this.CalcularDeuda(fecha, fechaDevuelto);
      this.usuarios.push({ ...this.newStudent });
      // Reset the form
      this.newStudent = {
        nombre: "",
        equipo: "",
        estado: "",
        fechaAdquisicion: "",
        fechaMaxima: "",
        fechaDevuelto: "",
        deuda: 0,
      };
    },
  },
  created() {
    this.usuarios.forEach((element) => {
      const fecha = new Date(element.fechaMaxima);
      const fechaDevuelto = new Date(element.fechaDevuelto);
      element.deuda = this.CalcularDeuda(fecha, fechaDevuelto);
    });
  },
};
</script>

<style scoped>
.container {
  background-color: white;
}

.header {
  background-color: #1590b8;
  text-align: center;
  padding: 20px;
}

.title {
  font-size: 2rem;
  color: white;
}

.table-container {
  margin-top: 5%;
  text-align: center;
}

.table {
  width: 100%;
  border-collapse: collapse;
  margin: auto;
}

table th,
table td {
  border: 1px solid #dddddd;
  text-align: center;
  padding: 8px;
}

th {
  background-color: #1590b8;
  color: white;
}

td {
  padding: 10px 15px !important;
}

.Entregado {
  background-color: green;
  color: #FFF;
}

.Pendiente {
  background-color: red;
  color: #FFF;
}

footer {
  margin-top: 10%;
  text-align: center;
}

a {
  color: royalblue;
}

.add-button {
  background-color: #1590b8;
  color: white;
  border: none;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 5px 2px;
  cursor: pointer;
  border-radius: 5px;
}
</style>
