<template>
  <div id="app">
    <UsersList 
      @selected="selectUser"
      @delete="deleteCartOfUser"
      :usersWithCart="Object.keys(cart)" />

    <hr v-if="selectedUser" />

    <FoodList 
      v-if="selectedUser" 
      @selected="addFood"
      :selectedItems="cart[selectedUser] || {}"/>

    <template  v-if="Object.keys(order).length">
      <hr />
      <table class="table is-striped is-fullwidth is-bordered">
        <tbody>
          <tr v-for="(value, key) in order" :key="key">
            <td>{{ value }}</td>
            <td>{{ key }}</td>
          </tr>
        </tbody>
      </table>
    </template>
    
    
  </div>
</template>

<script>

import UsersList from './UsersList'
import FoodList from './FoodList'
export default {
  name: 'app',
  data () {
    return {
      selectedUser: '',
      cart: {},
      prop: {
        'cafe-solo': 1,
        'mollete': 1
      }
    }
  },
  methods: {
    selectUser(user) {
      this.selectedUser = user
    },

    addFood (food) {
      if (!this.cart[this.selectedUser]) {
        this.$set(this.cart, this.selectedUser, {})
      }

      if (this.cart[this.selectedUser][food]) {
        this.$delete(this.cart[this.selectedUser], food)
      } else {
        this.$set(this.cart[this.selectedUser], food, 1)
      }
    },

    deleteCartOfUser (user) {
      this.selectedUser = ''
      this.$delete(this.cart, user)
    }
  },

  computed: {
    order () {
      let order = {}

      if (!this.cart) {
        return;
      }

      Object.keys(this.cart).forEach(person => {
        Object.keys(this.cart[person]).forEach(item => {
          if (order[item]) {
            order[item] += this.cart[person][item]
          } else {
            order[item] = this.cart[person][item]
          }
        })
      })

      return order
    }
  },
  mounted () {
    window.scrollTo(0, 1); 
  },
  components: {
    FoodList,
    UsersList
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 0.75rem;
}
</style>
