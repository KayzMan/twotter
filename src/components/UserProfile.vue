<template>
<div class="user-profile">
  <div class="user-profile_user_panel">
    <h1 class="user-profile_username">@{{ user.username }}</h1>
    <div class="user-profile_admin-badge" v-if="user.isAdmin">
      Admin
    </div>
    <div class="user-profile_follower-count">
      <strong>Followers: </strong> {{ followers }}
    </div>
    <form class="user-profile_create_twoot" @submit.prevent="createNewTwoot">
      <label for="newTwoot"><strong>New Twoot</strong></label>
      <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>

      <div class="user-profile_create-twoot-type">
        <label for="newTwootType"><strong>Type: </strong></label>
        <select id="newTwootType" v-model="selectedTwootType">
          <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
            {{ option.name }}
          </option>
        </select>
      </div>

      <button>
        Twoot!!
      </button>
    </form>
  </div>
  <div class="user-profile_twoots-wrapper">
    <TwootItem :username="user.username" v-for="twoot in user.twoots" :key="twoot.id" :twoot="twoot" @favourite="toggleFavourite"/>
  </div>
</div>
</template>

<script>
import TwootItem from "@/components/TwootItem";

export default {
  name: "UserProfile",
  components: { TwootItem },
  data(){
    return{
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Twoot'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: '_NgoniKayzMan',
        firstname: 'Ngoni',
        lastname: 'KayzMan',
        email: 'ngonik8@gmail.com',
        isAdmin: true,
        twoots: [
          { id: 1, content: "Twooter is Amazing" },
          { id: 2, content: "Don't forget to sign yourself up!" }
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount)
        console.log(`${this.user.username} has gained a follower!`)
    }
  },
  computed: {
    fullName(){
      return `${this.user.username} ${this.user.lastname}`
    }
  },
  methods: {
    followUser(){
      this.followers++
    },
    toggleFavourite(id){
      console.log(`Favourited Tweet #${id}`)
    },
    createNewTwoot(){
      if(this.newTwootContent && this.selectedTwootType !== 'draft'){
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent
        })
        this.newTwootContent = "";
      }
    }
  },
  mounted() { //a lifecycle hook
    this.followUser()
  }
}
</script>

<style scoped>
.user-profile{
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile_user_panel{
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
}

.user-profile_admin-badge{
  background-color: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  margin-top: 5px;
  margin-bottom: 5px;
  padding: 2px 10px;
  font-weight: bold;
}

h1{
  margin: 0;
}

.user-profile_create_twoot{
  padding-top: 20px;
  border-top: 1px solid #DFE3E8;
  display: flex;
  flex-direction: column;
}
</style>