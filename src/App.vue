<template>
  <div>
    <div class="container-fluid navbar-inverse bg-inverse">
      <div class="row">
        <div class="col">
          <div class="navbar">
            <form class="form-inline  d-flex justify-content-end">
              <div v-if="!signComplete">
                <button class="btn btn-outline-success mr-3" type="button" @click="switchSign('sign-in')">Войти</button>
                <button class="btn btn-outline-success" type="button" @click="switchSign('sign-up')">Регистрация</button>
              </div>
              <span v-else>{{ email }}</span>
            </form>
          </div>
        </div>
      </div>
    </div>
    <div class="container" v-if="!isMainPage">
      <div class="row">
        <div class="col">
          <sign-in v-if="sign == 'sign-in'" @addUser="isMainPage = $event.MainPage, signComplete = $event.complete
          ,email = $event.email, uid = $event.uid "></sign-in>
          <sign-up v-else @regSuccess="sign = $event"></sign-up>
        </div>
      </div>
    </div>
    <div class="container" v-else>
      <div class="row">
        <div class="col">
          <main-page :uid="uid"></main-page>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SignIn from './components/SignIn.vue'
import SignUp from './components/SignUp.vue'
import MainPage from './components/MainPage.vue'
export default {
  name: 'app',
  data () {
    return {
      sign: 'sign-in',
      isMainPage: false,
      signComplete: false,
      email: '',
      uid: ''
    }
  },
  components:{
    SignIn,
    SignUp,
    MainPage
  },
  methods:{
    switchSign(currentSing){
      this.sign = currentSing;
    }
  }

}
</script>

<style lang="scss">
    span{
      color: #ffffff;
    }
</style>
