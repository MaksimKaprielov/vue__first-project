<template>
  <div id="app">
    <div class="inputs">
      <input type="text" v-model="userName" placeholder="Имя" autocomplete="off">
      <input type="password" v-model="userPass" placeholder="Пароль" autocomplete="off">
      <input type="email" v-model="userEmail" placeholder="Email" autocomplete="off">
      <button @click="sendData()">Отправить</button>
      <p className="error"> {{ error }} </p>

      <div className="result" v-if="users.length == 0">
        <p className="result__users">Пользователи не найдены</p>
      </div>

      <div className="result" v-else-if="users.length == 1">
        <p className="result__users">Имеется один пользователь</p>
      </div>

      <div className="result" v-else>
        <p className="result__users">Имеется больше одного пользователя</p>
      </div>

      <div className="result" v-for="(el, index) in users" :key="index">
        <h3 className="result__name"> Имя: <span>{{ el.name }}</span></h3>
        <p className="result__email"> Email: <span>{{ el.email }}</span></p>
        <p className="result__pass">Pass: <span>{{ el.pass }}</span></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      error: '',
      userName: '',
      userPass: '',
      userEmail: ''
    }
  },
  methods: {
    sendData() {
      if (this.userName == '') {
        this.error = "Имя не введено";
        return;
      } else if(this.userPass == '') {
        this.error = "Пароль не введен";
        return;
      } else if(this.userEmail == '') {
        this.error = "Email не введен";
        return;
      } 

      this.error = '';

      this.users.push({
        name: this.userName,
        pass: this.userPass,
        email: this.userEmail
      })
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');
@import url(/assets/css/reset.css);
#app {
  padding: 40px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.inputs {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.inputs input {
  padding: 15px 20px;
  border-radius: 20px;
  border: 1px solid #e040fb;

  font-size: 16px;
  font-weight: 400;
  color: #000;
}

.inputs input::focused {
  border: 1px solid #aca9a9;
}

.inputs button {
  background-color: #e040fb;
  padding: 15px 20px;
  border-radius: 20px;
  border: 1px solid #e040fb;
  color: #fff;

  font-size: 16px;
  font-weight: 600;

  transition: all .3s ease;
}

.inputs button:hover {
  background-color: #fff;
  color: #e040fb;
  transition: all .3s ease;
}

.error {
  font-size: 16px;
  color: #ff0000;
}

.result {
  display: flex;
  flex-direction: column;
  gap: 10px;

  background-color: #e040fb;
  padding: 20px;
  border-radius: 20px;
}

.result__name, .result__email, .result__pass {
  font-size: 16px;
  font-weight: 400;
  color: #fff;
}

.result__name span, .result__email span, .result__pass span {
  font-size: 20px;
  font-weight: 600;
}

.result__users {
  font-size: 16px;
  font-weight: 400;
  color: #fff;
}
</style>