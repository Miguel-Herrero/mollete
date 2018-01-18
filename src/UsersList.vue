<template>
<section>
  <div class="columns">
    <div class="column" 
      v-for="user in users" 
      :key="user" 
      @click="selected(user)">
      <div 
        class="notification is-link" 
        :class="{
          'is-success': selectedUser === user,
          'is-info': selectedUser !== user && usersWithCart.indexOf(user) >= 0
        }">
        <strong>{{ user }}</strong>
        <button v-if="selectedUser === user" @click="$emit('delete', user)" class="delete"></button>
      </div>
    </div>
  </div>
</section>
</template>

<script>
export default {
  props: {
    usersWithCart: {
      type: Array
    }
  },
  data () {
    return {
      users: [ 'Fran', 'Josemi', 'Juan Carlos', 'Luismi', 'Marcos', 'Miguel' ],
      selectedUser: ''
    }
  },
  methods: {
    selected (user) {
      this.selectedUser = user
      this.$emit('selected', user)
    }
  }
}
</script>

<style scoped>
.column {
  padding-bottom: 0.15rem;
  padding-top: 0.15rem;
}
</style>

