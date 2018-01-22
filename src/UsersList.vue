<template>
<section>
  <div class="columns is-mobile is-multiline">
    <div class="column is-half-mobile" 
      v-for="user in users" 
      :key="user" 
      @click.stop="selected(user)">
      <div 
        class="notification" 
        :class="{
          'is-success': selectedUser === user,
          'is-primary': selectedUser !== user && usersWithCart.indexOf(user) >= 0,
          'is-link': selectedUser !== user && usersWithCart.indexOf(user) < 0
        }">
        <strong>{{ user }}</strong>
        <button v-if="selectedUser === user" @click.stop="$emit('delete', user)" class="delete is-large"></button>
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
      users: [ 'Fran', 'Josemi', 'J.Carlos', 'Luismi', 'Marcos', 'Miguel', 'Jokin' ],
      selectedUser: ''
    }
  },
  methods: {
    selected (user) {
      if (this.selectedUser === user) {
        this.selectedUser = ''
        this.$emit('selected', '')
      } else {
        this.selectedUser = user
        this.$emit('selected', user)
      }
    }
  }
}
</script>

<style scoped>
.column {
  padding-bottom: 0.15rem;
  padding-top: 0.15rem;
}
.notification {
  padding-top: 1rem;
  padding-bottom: 1rem;
}
</style>

