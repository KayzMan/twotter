<template>
<div class="twoot-item" @click="favouriteTwoot(twoot.id)">
  <div class="user-profile_twoot">
    <div class="twoot-item_user">
      @{{ username }}
    </div>
    <div class="twoot-item_content">
      {{ twoot.content }}
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true
    },
    twoot: {
      type: Object,
      required: true
    }
  },
  methods: {
    favouriteTwoot(id){
      this.$emit('favourite', id)
    }
  }
}
</script>

<style scoped>
.twoot-item{
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  width: 80%;
  border: 1px solid #DFE3E8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all .25s ease;
  margin: 10px;
}

.twoot-item:hover{
  transform: scale(1.1, 1.1);
}

.twoot-item_user{
  font-weight: bold;
}
</style>