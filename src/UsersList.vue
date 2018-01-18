<template>
<section>
  <div class="columns">
    <div class="column" 
      v-for="user in users" 
      :key="user" 
      @click="selected(user)">
      <div class="notification is-link" :class="{'is-success': selectedUser === user}">
        <strong>{{ user }}</strong>
        <button v-if="selectedUser === user" @click="$emit('delete', user)" class="delete"></button>
      </div>
    </div>
  </div>
</section>
</template>

<script>
export default {
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
