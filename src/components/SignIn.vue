<template>
  <form class="mt-5" @submit.prevent="enterUser">
      <div class="form-group">
          <label for="email">Ваш email</label>
          <input type="email" class="form-control" id="email" placeholder="Введите email" required v-model="user.email">
      </div>
      <div class="form-group">
          <label for="password">Ваш пароль</label>
          <input type="password" class="form-control" id="password" placeholder="Введите пароль" required v-model="user.password">
      </div>
      <button type="submit" class="btn btn-primary">Войти</button>
  </form>
</template>

<<script>
export default {
  data(){
      return{
          user: {
              email: '',
              password: ''
          }
      }
  },
  methods: {
      enterUser(){
          firebase.auth().signInWithEmailAndPassword(this.user.email, this.user.password)
            .then( response => {
                console.log(response);
                const sett = {
                    email: response.email,
                    uid: response.uid,
                    MainPage: true,
                    complete: true 
                }
                this.$emit('addUser',sett);
            })
            .catch(error =>{
                console.log(error);
            })            
      }
  }
}
</script>

