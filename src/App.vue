<template>

  <body>
    <div id="nav">

    
      <router-link to="/tabla" id="linknav" v-if="is_auth">
        Registros</router-link>
      |
      <router-link to="/censoIndigena" id="linknav">Agregar</router-link>
      |
      <router-link to="" id="linknav">Estadisticas</router-link>|

      <!--router-link to="/registrar" id="linknav">Agregar 2</router-link-->
    

      <div class="registrarbutton">
        <button id="buttonreg" v-if="!is_auth" :key="is_auth" v-on:click="loadLogin">
          Iniciar Sesion
        </button>
      </div>

      <div class="registrarbutton" id="buttoncerrar">
        <button to="/form" id="buttonreg" v-if="is_auth" :key="is_auth"  v-on:click="logOut">
          Salir
        </button>
      </div>

      <div class="title">
        <h2>Censo Indigena</h2>
      </div>
    </div>

    <div id="content">

      <router-view v-on:completedLogin="completedLogin" v-on:logOut="logOut" v-on:msjLogOutSuaveReReenv="logOutSuave">
      </router-view>
    </div>

    <div class="footer">
      <h2>Mision TIC 2021 - Equipo 2, Grupo 8</h2>
    </div>
  </body>

</template>
<script>
export default {
  name: "App",
  //direccionBack: "https://censoindigena.herokuapp.com/",
  direccionBack: "http://localhost:8000/",

  data: function() {
    return {
      username: localStorage.getItem("email"),
      is_auth: localStorage.getItem("is_auth") == undefined? false : localStorage.getItem("is_auth"),
    };
  },
  components: {},

  methods: {
    verifyAuth: function() {
      this.is_auth = localStorage.getItem("is_auth") || false;
      if (this.is_auth == false) {
        this.$router.push({ name: "Form" });
      } else {
        this.$router.push({ name: "Tabla" });
      }
    },

    loadLogin: function() {
      this.$router.push({ name: "Form" });
    },

    completedLogin: function(data) {
      localStorage.setItem("is_auth", true);
      localStorage.setItem("email", data.email);
      localStorage.setItem("token_access", data.token_access);
      localStorage.setItem("token_refresh", data.token_refresh);
      alert("Autenticacion exitosa");
      this.verifyAuth();
    },

    logOut: function() {
      localStorage.clear();
      alert("Sesión terminada");
      this.verifyAuth();
    },

    logOutSuave: function() {
      localStorage.clear();
      alert("Sesión terminada");
      this.is_auth = false;
      localStorage.setItem("is_auth", false);

    }
  },

  created: function() {
    this.verifyAuth();
  },
};
</script>



<style>
* {
  /*border: 1px solid;*/
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 9px;
  background-color: rgb(127, 157, 255);
  width: 99%;
  padding-bottom: 15px;
  padding-top: 15px;
}

#nav {
  font-weight: bold;
  color: #2c3e50;
  height: 30px;
}

#nav #linknav {
  position: relative;
  color: #f4f7fa;
  padding: 28px;
  letter-spacing: 1px;
  text-decoration: none;
}

#nav #linknav:after {
  content: "";
  position: absolute;
  background-color: #f1e53c;
  height: 3px;
  width: 0%;
  left: 0;
  bottom: 8px;
  transition: 0.5s;
}

#nav #linknav:hover:after {
  width: 100%;
}

#buttonreg {
  color: #f4f7fa;
  background-color: rgb(127, 157, 255);
  border: 2px solid;
  border-radius: 15px;
  border-color: #f1e53c;
  width: 120px;
  padding: 10px;
  margin: 0px;
  height: 45px;
  text-align: center;
  text-decoration: none;
  transition: 0.5s;
}

#buttonreg:hover {
  background-color: #eceff1;
  color: rgb(127, 157, 255);
}

.registrarbutton {
  position: absolute;
  width: 10%;
  margin-left: 80%;
  margin-top: -25px;
}

.title {
  position: relative;
  width: 500px;
  margin-top: -45px;
  padding-top: 0px;
  color: #f4f7fa;
}

#content {
  height: 878px;
}

.footer {
  color: #eceff1;
  padding: 9px;
  width: 99%;
  height: 55px;
  background-color: rgb(127, 157, 255);
}

body {
  margin: 0;
  padding: 0;
}

button {
  cursor: pointer;
}

.botonDelete {
  background-color: rgb(250, 124, 124);
}

.botonDelete:hover {
  background-color: rgb(248, 46, 46);
}
</style>
