<template>
  <form class="mt-5" @submit.prevent="registerUser">
      <div class="form-group">
          <label for="email">Ваш email:</label>
          <input class="form-control" id="email" type="email" placeholder="Введите email" required v-model="user.email">
      </div>
      <div class="form-group">
          <label for="password">Ваш пароль:</label>
          <input class="form-control" id="password" type="password" placeholder="Введите пароль" required v-model="user.password">
      </div>
      <div class="form-group">
          <label for="password2">Повторите пароль:</label>
          <input class="form-control" id="password2" type="password" placeholder="Повторите пароль" required v-model="user.confirmPassword">
      </div>
      <div class="alert alert-danger" role="alert" v-if="error">
          <strong>Oups!</strong> Пароли не совпадают или вы забыли их ввести
      </div>
      <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
  </form>
</template>

<script>
export default {
  name: 'singUp',
  data(){
      return{
          user: {
              email: '',
              password: '',
              confirmPassword: ''
          },
          error: false
        }
    },
      methods: {
          registerUser(){
              if(this.user.password !== this.user.confirmPassword || this.user.password.lenght < 6){
                  this.error = true;
              }
              else{
                  firebase.auth().createUserWithEmailAndPassword(this.user.email,this.user.password)
                    .then( () => {
                        this.$emit('regSuccess', 'sign-in');
                    })
                    .catch(error =>{
                        console.log(error);
                    })
              }
          }
      }
  }
</script>

